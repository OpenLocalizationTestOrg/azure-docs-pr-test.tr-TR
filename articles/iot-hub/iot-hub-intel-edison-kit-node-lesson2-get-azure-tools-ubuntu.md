---
title: "Intel Edison'u (düğüm) tooAzure IOT - Ders 2 bağlanın: Azure Araçları (Ubuntu) | Microsoft Docs"
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
ms.openlocfilehash: ca2996b779a4d3cde833c5f2824d19ec46241bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="931ba-104">Azure Araçları (Ubuntu 16.04) alın</span><span class="sxs-lookup"><span data-stu-id="931ba-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="931ba-105">[Windows 7 ve üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="931ba-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="931ba-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="931ba-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="931ba-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="931ba-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="931ba-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="931ba-108">What you will do</span></span>
<span data-ttu-id="931ba-109">Hello Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="931ba-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="931ba-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="931ba-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="931ba-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="931ba-111">What you will learn</span></span>
<span data-ttu-id="931ba-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="931ba-112">In this article, you will learn:</span></span>
* <span data-ttu-id="931ba-113">Nasıl tooinstall Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="931ba-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="931ba-114">Nasıl tooadd hello Azure CLI IOT GUID'sinin.</span><span class="sxs-lookup"><span data-stu-id="931ba-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="931ba-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="931ba-115">What you need</span></span>
* <span data-ttu-id="931ba-116">Bir Internet bağlantısı olan bir Ubuntu bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="931ba-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="931ba-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="931ba-117">An active Azure subscription.</span></span> <span data-ttu-id="931ba-118">Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz deneme sürümü hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="931ba-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="931ba-119">Hello Azure CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="931ba-119">Install hello Azure CLI</span></span>
<span data-ttu-id="931ba-120">Hello Azure CLI, Azure, komut satırı tooprovision doğrudan toowork etkinleştirme için birden çok platformlu bir komut satırı deneyimi sağlar ve kaynakları yönetin.</span><span class="sxs-lookup"><span data-stu-id="931ba-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="931ba-121">tooinstall en son Azure CLI Merhaba, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="931ba-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="931ba-122">Bir terminal penceresi komutlarda aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="931ba-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="931ba-123">Beş dakika tooinstall hello Azure CLI alabilir.</span><span class="sxs-lookup"><span data-stu-id="931ba-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="931ba-124">Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="931ba-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="931ba-125">Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="931ba-125">You should see hello following output if hello installation is successful.</span></span>

![Başarı belirten bir çıkış](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="931ba-127">Özet</span><span class="sxs-lookup"><span data-stu-id="931ba-127">Summary</span></span>
<span data-ttu-id="931ba-128">Hello Azure CLI yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="931ba-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="931ba-129">Sonraki göreviniz toocreate olan Azure IOT hub ve cihaz kimliğini kullanarak Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="931ba-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="931ba-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="931ba-130">Next steps</span></span>
<span data-ttu-id="931ba-131">[IOT hub'ınızı oluşturun ve Intel Edison'u kaydedin][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="931ba-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
