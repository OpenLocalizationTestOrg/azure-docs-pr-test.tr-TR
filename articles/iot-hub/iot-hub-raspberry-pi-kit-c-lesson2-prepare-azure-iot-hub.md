---
title: "Connect Raspberry pi (C) tooAzure IOT - Ders 2: kayıt cihazı | Microsoft Docs"
description: "Bir kaynak grubu oluşturmak, Azure IOT hub oluşturma ve Pi hello Azure IOT hub'hello Azure CLI kullanarak kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "pi bulut Böğürtlenli pi bulut Bağlan"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 473658c5a8e1e0d4cfced0efafbad2640a1e0696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="99380-104">IOT hub'ınızı oluşturun ve Raspberry Pi 3 kaydedin</span><span class="sxs-lookup"><span data-stu-id="99380-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="99380-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="99380-105">What you will do</span></span>
* <span data-ttu-id="99380-106">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="99380-106">Create a resource group.</span></span>
* <span data-ttu-id="99380-107">Azure IOT hub'ınızı hello kaynak grubunda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="99380-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="99380-108">Raspberry Pi 3 toohello Azure IOT hub'hello Azure komut satırı arabirimi (Azure CLI) kullanarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="99380-108">Add Raspberry Pi 3 toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="99380-109">Hello Azure CLI tooadd PI tooyour IOT hub'ı kullandığınızda, hello hizmeti hello hizmetiyle Pi tooauthenticate için bir anahtar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99380-109">When you use hello Azure CLI tooadd Pi tooyour IoT hub, hello service generates a key for Pi tooauthenticate with hello service.</span></span> <span data-ttu-id="99380-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="99380-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="99380-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="99380-111">What you will learn</span></span>
<span data-ttu-id="99380-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="99380-112">In this article, you will learn:</span></span>
* <span data-ttu-id="99380-113">Nasıl toouse hello Azure CLI toocreate IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="99380-113">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="99380-114">Nasıl toocreate IOT hub'ınızdaki pi bir cihaz kimliği.</span><span class="sxs-lookup"><span data-stu-id="99380-114">How toocreate a device identity for Pi in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="99380-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="99380-115">What you need</span></span>
* <span data-ttu-id="99380-116">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="99380-116">An Azure account</span></span>
* <span data-ttu-id="99380-117">Mac veya bir Windows bilgisayar hello ile Azure CLI yüklenmiş</span><span class="sxs-lookup"><span data-stu-id="99380-117">A Mac or a Windows computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="99380-118">IOT hub'ınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="99380-118">Create your IoT hub</span></span>
<span data-ttu-id="99380-119">Azure IOT Hub bağlanmak, izlemek ve milyonlarca IOT varlıklarını yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="99380-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="99380-120">toocreate IOT hub'ınızı şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="99380-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="99380-121">İçinde tooyour hello aşağıdaki komutu çalıştırarak Azure hesabı imzalayın:</span><span class="sxs-lookup"><span data-stu-id="99380-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="99380-122">Kullanılabilir aboneliklerin bir başarılı oturum açma işleminden sonra listelenir.</span><span class="sxs-lookup"><span data-stu-id="99380-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="99380-123">Merhaba aşağıdaki komutu çalıştırarak toouse istediğiniz hello varsayılan abonelik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="99380-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="99380-124">`subscription ID or name`Merhaba Hello çıktısında bulunabilir `az login` veya hello `az account list` komutu.</span><span class="sxs-lookup"><span data-stu-id="99380-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="99380-125">Merhaba sağlayıcıyı hello aşağıdaki komutu çalıştırarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="99380-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="99380-126">Kaynak sağlayıcıları, uygulamanız için kaynakları sağlayan hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="99380-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="99380-127">Merhaba sağlayıcısı teklifleri hello Azure kaynak dağıtmadan önce hello sağlayıcısı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="99380-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="99380-128">Adlı bir kaynak grubu hello Batı ABD bölgesinde hello aşağıdaki komutu çalıştırarak IOT örnek oluşturun:</span><span class="sxs-lookup"><span data-stu-id="99380-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="99380-129">`westus`kaynak grubu oluşturma hello bir konumdur.</span><span class="sxs-lookup"><span data-stu-id="99380-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="99380-130">Başka bir konuma toouse istiyorsanız çalıştırabilirsiniz `az account list-locations -o table` toosee tüm hello konumları Azure destekler.</span><span class="sxs-lookup"><span data-stu-id="99380-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>
 
5. <span data-ttu-id="99380-131">IOT hub'ı hello aşağıdaki komutu çalıştırarak hello IOT örnek kaynak grubunda oluşturun:</span><span class="sxs-lookup"><span data-stu-id="99380-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="99380-132">Varsayılan olarak, hello aracı hello ücretsiz fiyatlandırma katmanında bir IOT hub'ı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99380-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="99380-133">Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="99380-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="99380-134">IOT hub'ınızı Hello adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="99380-134">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="99380-135">Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99380-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="99380-136">IOT hub'ınıza pi kaydetme</span><span class="sxs-lookup"><span data-stu-id="99380-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="99380-137">IOT hub'ından ileti alıp tooyour IOT hub'ı iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="99380-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="99380-138">Pi hub'ınıza çalışan aşağıdaki komutla kaydedin:</span><span class="sxs-lookup"><span data-stu-id="99380-138">Register Pi in your hub by running following command:</span></span>

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a><span data-ttu-id="99380-139">Özet</span><span class="sxs-lookup"><span data-stu-id="99380-139">Summary</span></span>
<span data-ttu-id="99380-140">IOT hub'ı oluşturulur ve Pi cihaz kimliğiyle IOT hub'ınıza kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="99380-140">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="99380-141">Pi tooyour IOT hub'ından toosend nasıl iletileri hazır toolearn demektir.</span><span class="sxs-lookup"><span data-stu-id="99380-141">You're ready toolearn how toosend messages from Pi tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99380-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99380-142">Next steps</span></span>
<span data-ttu-id="99380-143">[Bir Azure işlevi uygulama ve Azure Storage hesabı tooprocess ve deposu IOT hub'ı iletileri oluşturmak](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="99380-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

