---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 2: kayıt cihazı | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure IOT hub'ı Internet şeyler bulut, azure IOT hub oluşturma aygıt, tı sensortag, tı Boşalt"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 685a479583f5f11f57bef22dc5881285bb1f70d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="fa145-103">Azure IOT hub'ınızı oluşturun ve Cihazınızı kaydedin</span><span class="sxs-lookup"><span data-stu-id="fa145-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="fa145-104">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="fa145-104">What you will do</span></span>

- <span data-ttu-id="fa145-105">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa145-105">Create a resource group</span></span>
- <span data-ttu-id="fa145-106">İlk IOT hub'ınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa145-106">Create your first IoT hub</span></span>
- <span data-ttu-id="fa145-107">Cihazınızı IOT hub'ınıza Azure CLI kullanarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fa145-107">Register your device in your IoT hub by using the Azure CLI.</span></span> 

<span data-ttu-id="fa145-108">IOT hub'ınıza Cihazınızı kaydettiğinizde Azure IOT Hub hizmeti hizmeti ile kimlik doğrulaması için kullanılacak cihazınız için bir anahtar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fa145-108">When you register your device in your IoT hub, the Azure IoT Hub service generates a key for your device to use to authenticate with the service.</span></span> 

<span data-ttu-id="fa145-109">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="fa145-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fa145-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="fa145-110">What you will learn</span></span>

<span data-ttu-id="fa145-111">Bu alıştırmanın ilerisinde şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="fa145-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="fa145-112">IOT hub'ı oluşturmak için Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="fa145-112">How to use the Azure CLI to create an IoT hub.</span></span>
- <span data-ttu-id="fa145-113">Bir IOT hub ' bir cihazı kaydetmek nasıl.</span><span class="sxs-lookup"><span data-stu-id="fa145-113">How to register a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fa145-114">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="fa145-114">What you need</span></span>

- <span data-ttu-id="fa145-115">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="fa145-115">An active Azure subscription.</span></span> <span data-ttu-id="fa145-116">Bir Azure hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="fa145-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="fa145-117">Azure CLI'ın yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa145-117">You should have the Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="fa145-118">IoT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa145-118">Create an IoT hub</span></span>

<span data-ttu-id="fa145-119">IOT hub'ı oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="fa145-119">To create an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="fa145-120">Aşağıdaki komutu çalıştırarak Azure hesabınızda oturum açın:</span><span class="sxs-lookup"><span data-stu-id="fa145-120">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="fa145-121">Kullanılabilir aboneliklerin bir başarılı oturum açma işleminden sonra listelenir.</span><span class="sxs-lookup"><span data-stu-id="fa145-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="fa145-122">Aşağıdaki komutu çalıştırarak kullanmak istediğiniz Azure aboneliği varsayılan ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="fa145-122">Set the default Azure subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="fa145-123">`subscription ID or name`çıktısında bulunabilir `az login` veya `az account list` komutu.</span><span class="sxs-lookup"><span data-stu-id="fa145-123">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="fa145-124">Aşağıdaki komutu çalıştırarak sağlayıcıyı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fa145-124">Register the provider by running the following command.</span></span> <span data-ttu-id="fa145-125">Kaynak sağlayıcıları, uygulamanız için kaynakları sağlayan hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="fa145-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="fa145-126">Sağlayıcısı sunar Azure kaynak dağıtabilmeniz için önce sağlayıcı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa145-126">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="fa145-127">Adlı bir kaynak grubu oluşturmak `iot-gateway` aşağıdaki komutu çalıştırarak Batı ABD bölgesindeki:</span><span class="sxs-lookup"><span data-stu-id="fa145-127">Create a resource group named `iot-gateway` in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="fa145-128">`westus`kaynak grubu oluşturma konumdur.</span><span class="sxs-lookup"><span data-stu-id="fa145-128">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="fa145-129">Başka bir konuma kullanmak istiyorsanız, çalıştırabilirsiniz `az account list-locations -o table` tüm konumları Azure destekler.</span><span class="sxs-lookup"><span data-stu-id="fa145-129">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="fa145-130">Bir IOT hub'ı oluşturmak `iot-gateway` aşağıdaki komutu çalıştırarak kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="fa145-130">Create an IoT hub in the `iot-gateway` resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="fa145-131">Varsayılan olarak, aracı, IOT hub'ı ücretsiz fiyatlandırma katmanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fa145-131">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="fa145-132">Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="fa145-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="fa145-133">IOT hub'ınızı adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa145-133">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="fa145-134">Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa145-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="fa145-135">IOT hub'ınıza Cihazınızı kaydedin</span><span class="sxs-lookup"><span data-stu-id="fa145-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="fa145-136">IOT hub'ından ileti alıp IOT hub'ına iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="fa145-136">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="fa145-137">Cihazınızı IOT hub'ınıza çalışan aşağıdaki komutla kaydedin:</span><span class="sxs-lookup"><span data-stu-id="fa145-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="fa145-138">Özet</span><span class="sxs-lookup"><span data-stu-id="fa145-138">Summary</span></span>

<span data-ttu-id="fa145-139">IOT hub'ı oluşturulur ve mantıksal Cihazınızı cihaz kimliğiyle IOT hub'ınıza kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="fa145-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="fa145-140">Yapılandırma ve verileri bulutta IOT hub'ınızı fiziksel cihazınızdan göndermek için bir ağ geçidi örnek uygulamayı çalıştırma hakkında bilgi edinmek hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="fa145-140">You're ready to learn how to configure and run a gateway sample application to send data from your physical device to your IoT hub in the cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa145-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fa145-141">Next steps</span></span>
[<span data-ttu-id="fa145-142">Yapılandırma ve bırak örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="fa145-142">Configure and run a BLE sample app</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)