---
featureFlags: usabilla
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 2 bağlanın: kayıt cihazı | Microsoft Docs"
description: "Bir kaynak grubu oluşturmak, Azure IOT hub oluşturma ve Azure CLI kullanarak hello IOT Hub kimlik kayıt defteri Pi kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "pi bulut Böğürtlenli pi bulut Bağlan"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="e61bd-104">IOT hub'ınızı oluşturun ve Raspberry Pi 3 kaydedin</span><span class="sxs-lookup"><span data-stu-id="e61bd-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e61bd-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="e61bd-105">What you will do</span></span>
* <span data-ttu-id="e61bd-106">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e61bd-106">Create a resource group.</span></span>
* <span data-ttu-id="e61bd-107">Azure IOT hub'ınızı hello kaynak grubunda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e61bd-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="e61bd-108">Raspberry Pi 3 toohello Azure IOT hub'hello Azure komut satırı arabirimi (Azure CLI) kullanarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e61bd-108">Add Raspberry Pi 3 toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="e61bd-109">Azure CLI tooadd PI tooyour IOT hub'ı kullandığınızda, hello hizmeti hello hizmetiyle Pi tooauthenticate için bir anahtar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e61bd-109">When you use Azure CLI tooadd Pi tooyour IoT hub, hello service generates a key for Pi tooauthenticate with hello service.</span></span> <span data-ttu-id="e61bd-110">Herhangi bir sorun varsa, hello çözümlerini arama [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e61bd-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e61bd-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="e61bd-111">What you will learn</span></span>
<span data-ttu-id="e61bd-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="e61bd-112">In this article, you will learn:</span></span>
* <span data-ttu-id="e61bd-113">Nasıl toouse Azure CLI toocreate IOT hub'ı</span><span class="sxs-lookup"><span data-stu-id="e61bd-113">How toouse Azure CLI toocreate an IoT hub</span></span>
* <span data-ttu-id="e61bd-114">Nasıl toocreate IOT hub'ınızdaki pi bir cihaz kimliği</span><span class="sxs-lookup"><span data-stu-id="e61bd-114">How toocreate a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e61bd-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="e61bd-115">What you need</span></span>
* <span data-ttu-id="e61bd-116">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="e61bd-116">An Azure account</span></span>
* <span data-ttu-id="e61bd-117">Mac veya bir Windows bilgisayar hello ile Azure CLI yüklenmiş</span><span class="sxs-lookup"><span data-stu-id="e61bd-117">A Mac or a Windows computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="e61bd-118">IOT hub'ınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e61bd-118">Create your IoT hub</span></span>
<span data-ttu-id="e61bd-119">Azure IOT Hub bağlanmak, izlemek ve milyonlarca IOT varlıklarını yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e61bd-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="e61bd-120">toocreate IOT hub'ınızı şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e61bd-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="e61bd-121">İçinde tooyour hello aşağıdaki komutu çalıştırarak Azure hesabı imzalayın:</span><span class="sxs-lookup"><span data-stu-id="e61bd-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="e61bd-122">Kullanılabilir aboneliklerin bir başarılı oturum açma işleminden sonra listelenir.</span><span class="sxs-lookup"><span data-stu-id="e61bd-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="e61bd-123">Merhaba aşağıdaki komutu çalıştırarak toouse istediğiniz hello varsayılan abonelik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e61bd-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="e61bd-124">`subscription ID or name`Merhaba Hello çıktısında bulunabilir `az login` veya hello `az account list` komutu.</span><span class="sxs-lookup"><span data-stu-id="e61bd-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="e61bd-125">Merhaba sağlayıcıyı hello aşağıdaki komutu çalıştırarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e61bd-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="e61bd-126">Kaynak sağlayıcıları, uygulamanız için kaynakları sağlayan hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="e61bd-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="e61bd-127">Merhaba sağlayıcısı teklifleri hello Azure kaynak dağıtmadan önce hello sağlayıcısı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e61bd-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="e61bd-128">Adlı bir kaynak grubu hello Batı ABD bölgesinde hello aşağıdaki komutu çalıştırarak IOT örnek oluşturun:</span><span class="sxs-lookup"><span data-stu-id="e61bd-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="e61bd-129">`westus`kaynak grubu oluşturma hello bir konumdur.</span><span class="sxs-lookup"><span data-stu-id="e61bd-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="e61bd-130">Başka bir konuma toouse istiyorsanız çalıştırabilirsiniz `az account list-locations -o table` toosee tüm hello konumları Azure destekler.</span><span class="sxs-lookup"><span data-stu-id="e61bd-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>
 
5. <span data-ttu-id="e61bd-131">IOT hub'ı hello aşağıdaki komutu çalıştırarak hello IOT örnek kaynak grubunda oluşturun:</span><span class="sxs-lookup"><span data-stu-id="e61bd-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="e61bd-132">Varsayılan olarak, hello aracı hello ücretsiz fiyatlandırma katmanında bir IOT hub'ı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e61bd-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="e61bd-133">Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="e61bd-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="e61bd-134">IOT hub'ınızı Hello adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e61bd-134">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="e61bd-135">Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e61bd-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="e61bd-136">IOT hub'ınıza pi kaydetme</span><span class="sxs-lookup"><span data-stu-id="e61bd-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="e61bd-137">IOT hub'ından ileti alıp tooyour IOT hub'ı iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="e61bd-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="e61bd-138">Azure CLI tooregister, Pi kullanabilir ve cihaz kimlik doğrulaması için otomatik olarak imzalanan bir X.509 sertifikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e61bd-138">You will use Azure CLI tooregister your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="e61bd-139">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e61bd-139">Run hello following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="e61bd-140">Özet</span><span class="sxs-lookup"><span data-stu-id="e61bd-140">Summary</span></span>
<span data-ttu-id="e61bd-141">IOT hub'ı oluşturulur ve Pi cihaz kimliğiyle IOT hub'ınıza kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="e61bd-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="e61bd-142">Pi tooyour IOT hub'ından toosend nasıl iletileri hazır toolearn demektir.</span><span class="sxs-lookup"><span data-stu-id="e61bd-142">You're ready toolearn how toosend messages from Pi tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e61bd-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e61bd-143">Next steps</span></span>
[<span data-ttu-id="e61bd-144">Bir Azure işlevi uygulama ve bir Azure depolama hesabı tooprocess oluşturun ve IOT hub iletileri depolama</span><span class="sxs-lookup"><span data-stu-id="e61bd-144">Create an Azure function app and an Azure storage account tooprocess and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

