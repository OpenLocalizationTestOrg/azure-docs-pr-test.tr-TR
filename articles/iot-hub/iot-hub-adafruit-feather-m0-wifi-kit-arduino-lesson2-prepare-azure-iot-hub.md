---
title: "Arduino tooAzure IOT - Ders 2 bağlanın: kayıt cihazı | Microsoft Docs"
description: "Bir kaynak grubu oluşturmak, Azure IOT hub oluşturma ve Adafruit yumuşatma M0 WiFi hello Azure IOT hub'hello Azure CLI kullanarak kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "bağlanma arduino toocloud, azure IOT hub, Internet şeyler bulut azure IOT hub cihaz, arduino bulut oluşturma"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca362f9c143dd3a98bf47a66b63a9725a0ffc2d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a><span data-ttu-id="8c5b4-104">IOT hub'ınızı oluşturun ve Adafruit yumuşatma M0 WiFi Arduino panonuzu kaydedin</span><span class="sxs-lookup"><span data-stu-id="8c5b4-104">Create your IoT hub and register your Adafruit Feather M0 WiFi Arduino board</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8c5b4-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="8c5b4-105">What you will do</span></span>
* <span data-ttu-id="8c5b4-106">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-106">Create a resource group.</span></span>
* <span data-ttu-id="8c5b4-107">Azure IOT hub'ınızı hello kaynak grubunda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="8c5b4-108">Hello Azure komut satırı arabirimi (Azure CLI) kullanarak Arduino Panosu toohello Azure IOT hub'ınızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-108">Add your Arduino board toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="8c5b4-109">Arduino tablosu tooyour IOT hub'ınızı hello Azure CLI tooadd kullandığınızda, hello hizmeti, Arduino Panosu tooauthenticate hello hizmetiyle için bir anahtar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-109">When you use hello Azure CLI tooadd your Arduino board tooyour IoT hub, hello service generates a key for your Arduino board tooauthenticate with hello service.</span></span> <span data-ttu-id="8c5b4-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshoot].</span><span class="sxs-lookup"><span data-stu-id="8c5b4-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshoot].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8c5b4-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="8c5b4-111">What you will learn</span></span>
<span data-ttu-id="8c5b4-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="8c5b4-112">In this article, you will learn:</span></span>
* <span data-ttu-id="8c5b4-113">Nasıl toouse hello Azure CLI toocreate IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-113">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="8c5b4-114">Nasıl toocreate bir cihaz kimliği, Arduino için IOT hub'ınıza tahtası.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-114">How toocreate a device identity for your Arduino board in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8c5b4-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="8c5b4-115">What you need</span></span>
* <span data-ttu-id="8c5b4-116">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="8c5b4-116">An Azure account</span></span>
* <span data-ttu-id="8c5b4-117">Azure CLI yüklü bir bilgisayar hello</span><span class="sxs-lookup"><span data-stu-id="8c5b4-117">A computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="8c5b4-118">IOT hub'ınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c5b4-118">Create your IoT hub</span></span>
<span data-ttu-id="8c5b4-119">Azure IOT Hub bağlanmak, izlemek ve milyonlarca IOT varlıklarını yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="8c5b4-120">toocreate IOT hub'ınızı şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8c5b4-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="8c5b4-121">İçinde tooyour hello aşağıdaki komutu çalıştırarak Azure hesabı imzalayın:</span><span class="sxs-lookup"><span data-stu-id="8c5b4-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="8c5b4-122">Kullanılabilir aboneliklerin bir başarılı oturum açma işleminden sonra listelenir.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="8c5b4-123">Merhaba aşağıdaki komutu çalıştırarak toouse istediğiniz hello varsayılan abonelik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="8c5b4-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="8c5b4-124">`subscription ID or name`Merhaba Hello çıktısında bulunabilir `az login` veya hello `az account list` komutu.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="8c5b4-125">Merhaba sağlayıcıyı hello aşağıdaki komutu çalıştırarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="8c5b4-126">Kaynak sağlayıcıları, uygulamanız için kaynakları sağlayan hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="8c5b4-127">Merhaba sağlayıcısı teklifleri hello Azure kaynak dağıtmadan önce hello sağlayıcısı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="8c5b4-128">Adlı bir kaynak grubu hello Batı ABD bölgesinde hello aşağıdaki komutu çalıştırarak IOT örnek oluşturun:</span><span class="sxs-lookup"><span data-stu-id="8c5b4-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="8c5b4-129">`westus`kaynak grubu oluşturma hello bir konumdur.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="8c5b4-130">Başka bir konuma toouse istiyorsanız çalıştırabilirsiniz `az account list-locations -o table` toosee tüm hello konumları Azure destekler.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="8c5b4-131">IOT hub'ı hello aşağıdaki komutu çalıştırarak hello IOT örnek kaynak grubunda oluşturun:</span><span class="sxs-lookup"><span data-stu-id="8c5b4-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="8c5b4-132">Varsayılan olarak, hello aracı hello ücretsiz fiyatlandırma katmanında bir IOT hub'ı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="8c5b4-133">Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="8c5b4-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="8c5b4-134">IOT hub'ınızı Hello adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="8c5b4-135">Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-your-arduino-board-in-your-iot-hub"></a><span data-ttu-id="8c5b4-136">IOT hub'ınıza Arduino panonuzu kaydetme</span><span class="sxs-lookup"><span data-stu-id="8c5b4-136">Register your Arduino board in your IoT hub</span></span>
<span data-ttu-id="8c5b4-137">IOT hub'ından ileti alıp tooyour IOT hub'ı iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="8c5b4-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="8c5b4-138">Arduino panonuzu çalışan aşağıdaki komutu tarafından IOT hub'ınıza kaydedin:</span><span class="sxs-lookup"><span data-stu-id="8c5b4-138">Register your Arduino board in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="8c5b4-139">Özet</span><span class="sxs-lookup"><span data-stu-id="8c5b4-139">Summary</span></span>
<span data-ttu-id="8c5b4-140">IOT hub'ı oluşturulur ve Arduino panonuzu cihaz kimliğiyle IOT hub'ınıza kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-140">You've created an IoT hub and registered your Arduino board with a device identity in your IoT hub.</span></span> <span data-ttu-id="8c5b4-141">Arduino tablosu tooyour IOT hub'dan nasıl toosend iletileri hazır toolearn demektir.</span><span class="sxs-lookup"><span data-stu-id="8c5b4-141">You're ready toolearn how toosend messages from your Arduino board tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c5b4-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8c5b4-142">Next steps</span></span>
<span data-ttu-id="8c5b4-143">[Bir Azure işlevi uygulama ve Azure Storage hesabı tooprocess ve deposu IOT hub'ı iletileri oluşturmak][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="8c5b4-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md