---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 2: kayıt cihazı | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure IOT hub'ı Internet şeyler bulut, azure IOT hub oluşturma aygıt, tı sensortag, tı Boşalt"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d1052ed2fa9e022966e6e71fa2c7d4f18c333b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="904eb-103">Azure IOT hub'ınızı oluşturun ve Cihazınızı kaydedin</span><span class="sxs-lookup"><span data-stu-id="904eb-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="904eb-104">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="904eb-104">What you will do</span></span>

- <span data-ttu-id="904eb-105">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="904eb-105">Create a resource group</span></span>
- <span data-ttu-id="904eb-106">İlk IOT hub'ınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="904eb-106">Create your first IoT hub</span></span>
- <span data-ttu-id="904eb-107">Cihazınızı IOT hub'hello Azure CLI kullanarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="904eb-107">Register your device in your IoT hub by using hello Azure CLI.</span></span> 

<span data-ttu-id="904eb-108">IOT hub'ınıza Cihazınızı kaydederken hello Azure IOT Hub hizmeti, cihaz toouse tooauthenticate hello hizmetiyle için bir anahtar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="904eb-108">When you register your device in your IoT hub, hello Azure IoT Hub service generates a key for your device toouse tooauthenticate with hello service.</span></span> 

<span data-ttu-id="904eb-109">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="904eb-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="904eb-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="904eb-110">What you will learn</span></span>

<span data-ttu-id="904eb-111">Bu alıştırmanın ilerisinde şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="904eb-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="904eb-112">Nasıl toouse hello Azure CLI toocreate IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="904eb-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
- <span data-ttu-id="904eb-113">Nasıl tooregister bir IOT hub'ındaki bir aygıt.</span><span class="sxs-lookup"><span data-stu-id="904eb-113">How tooregister a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="904eb-114">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="904eb-114">What you need</span></span>

- <span data-ttu-id="904eb-115">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="904eb-115">An active Azure subscription.</span></span> <span data-ttu-id="904eb-116">Bir Azure hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="904eb-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="904eb-117">Hello Azure CLI yüklenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="904eb-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="904eb-118">IoT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="904eb-118">Create an IoT hub</span></span>

<span data-ttu-id="904eb-119">toocreate IOT hub'ı, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="904eb-119">toocreate an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="904eb-120">İçinde tooyour hello aşağıdaki komutu çalıştırarak Azure hesabı imzalayın:</span><span class="sxs-lookup"><span data-stu-id="904eb-120">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="904eb-121">Kullanılabilir aboneliklerin bir başarılı oturum açma işleminden sonra listelenir.</span><span class="sxs-lookup"><span data-stu-id="904eb-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="904eb-122">Merhaba varsayılan hello aşağıdaki komutu çalıştırarak toouse istediğiniz Azure aboneliği ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="904eb-122">Set hello default Azure subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="904eb-123">`subscription ID or name`Merhaba Hello çıktısında bulunabilir `az login` veya hello `az account list` komutu.</span><span class="sxs-lookup"><span data-stu-id="904eb-123">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="904eb-124">Merhaba sağlayıcıyı hello aşağıdaki komutu çalıştırarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="904eb-124">Register hello provider by running hello following command.</span></span> <span data-ttu-id="904eb-125">Kaynak sağlayıcıları, uygulamanız için kaynakları sağlayan hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="904eb-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="904eb-126">Merhaba sağlayıcısı teklifleri hello Azure kaynak dağıtmadan önce hello sağlayıcısı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="904eb-126">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="904eb-127">Adlı bir kaynak grubu oluşturmak `iot-gateway` hello aşağıdaki komutu çalıştırarak hello Batı ABD bölgesindeki:</span><span class="sxs-lookup"><span data-stu-id="904eb-127">Create a resource group named `iot-gateway` in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="904eb-128">`westus`kaynak grubu oluşturma hello bir konumdur.</span><span class="sxs-lookup"><span data-stu-id="904eb-128">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="904eb-129">Başka bir konuma toouse istiyorsanız çalıştırabilirsiniz `az account list-locations -o table` toosee tüm hello konumları Azure destekler.</span><span class="sxs-lookup"><span data-stu-id="904eb-129">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="904eb-130">Hello IOT hub oluşturma `iot-gateway` hello aşağıdaki komutu çalıştırarak kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="904eb-130">Create an IoT hub in hello `iot-gateway` resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="904eb-131">Varsayılan olarak, hello aracı hello ücretsiz fiyatlandırma katmanında bir IOT hub'ı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="904eb-131">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="904eb-132">Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="904eb-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="904eb-133">IOT hub'ınızı Hello adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="904eb-133">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="904eb-134">Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="904eb-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="904eb-135">IOT hub'ınıza Cihazınızı kaydedin</span><span class="sxs-lookup"><span data-stu-id="904eb-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="904eb-136">IOT hub'ından ileti alıp tooyour IOT hub'ı iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="904eb-136">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="904eb-137">Cihazınızı IOT hub'ınıza çalışan aşağıdaki komutla kaydedin:</span><span class="sxs-lookup"><span data-stu-id="904eb-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="904eb-138">Özet</span><span class="sxs-lookup"><span data-stu-id="904eb-138">Summary</span></span>

<span data-ttu-id="904eb-139">IOT hub'ı oluşturulur ve mantıksal Cihazınızı cihaz kimliğiyle IOT hub'ınıza kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="904eb-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="904eb-140">Tooconfigure ve fiziksel cihaz tooyour IOT hub'ınıza hello çalıştırma bir ağ geçidi örnek uygulama toosend verileri nasıl bulut hazır toolearn demektir.</span><span class="sxs-lookup"><span data-stu-id="904eb-140">You're ready toolearn how tooconfigure and run a gateway sample application toosend data from your physical device tooyour IoT hub in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="904eb-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="904eb-141">Next steps</span></span>
[<span data-ttu-id="904eb-142">Yapılandırma ve bir sanal cihaz bulut karşıya yükleme örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="904eb-142">Configure and run a simulated device cloud upload sample application</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)