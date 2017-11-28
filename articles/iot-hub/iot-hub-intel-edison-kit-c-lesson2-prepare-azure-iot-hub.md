---
title: "Azure IOT - Ders 2 Connect Intel Edison (C): kayıt cihazı | Microsoft Docs"
description: "Bir kaynak grubu oluşturmak, Azure IOT hub oluşturma ve Azure CLI kullanarak Azure IOT hub'ı Edison'u kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 52e3e4734dfd2b89f79b0c66683163e69b8e5f25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="69457-103">IOT hub'ınızı oluşturun ve Intel Edison'u kaydedin</span><span class="sxs-lookup"><span data-stu-id="69457-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="69457-104">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="69457-104">What you will do</span></span>
* <span data-ttu-id="69457-105">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="69457-105">Create a resource group.</span></span>
* <span data-ttu-id="69457-106">Azure IOT hub'ınızdaki kaynak grubunu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="69457-106">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="69457-107">Intel Edison'u Azure komut satırı arabirimi (Azure CLI) kullanarak Azure IOT hub'ına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="69457-107">Add Intel Edison to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="69457-108">IOT hub'ınıza Edison'u eklemek için Azure CLI kullandığınızda, hizmet Edison'u hizmeti ile kimlik doğrulaması için bir anahtar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69457-108">When you use the Azure CLI to add Edison to your IoT hub, the service generates a key for Edison to authenticate with the service.</span></span> <span data-ttu-id="69457-109">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="69457-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="69457-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="69457-110">What you will learn</span></span>
<span data-ttu-id="69457-111">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="69457-111">In this article, you will learn:</span></span>
* <span data-ttu-id="69457-112">IOT hub'ı oluşturmak için Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="69457-112">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="69457-113">IOT hub'ınıza Edison'u için bir cihaz kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="69457-113">How to create a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="69457-114">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="69457-114">What you need</span></span>
* <span data-ttu-id="69457-115">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="69457-115">An Azure account.</span></span> <span data-ttu-id="69457-116">Bir Azure hesabınız yoksa, oluşturma bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="69457-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="69457-117">Azure CLI'ın yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="69457-117">You should have the Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="69457-118">IOT hub'ınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="69457-118">Create your IoT hub</span></span>
<span data-ttu-id="69457-119">Azure IOT Hub bağlanmak, izlemek ve milyonlarca IOT varlıklarını yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="69457-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="69457-120">IOT hub'ınızı oluşturması için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="69457-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="69457-121">Aşağıdaki komutu çalıştırarak Azure hesabınızda oturum açın:</span><span class="sxs-lookup"><span data-stu-id="69457-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="69457-122">Kullanılabilir aboneliklerin bir başarılı oturum açma işleminden sonra listelenir.</span><span class="sxs-lookup"><span data-stu-id="69457-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="69457-123">Aşağıdaki komutu çalıştırarak kullanmak istediğiniz varsayılan abonelik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="69457-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="69457-124">`subscription ID or name`çıktısında bulunabilir `az login` veya `az account list` komutu.</span><span class="sxs-lookup"><span data-stu-id="69457-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="69457-125">Aşağıdaki komutu çalıştırarak sağlayıcıyı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="69457-125">Register the provider by running the following command.</span></span> <span data-ttu-id="69457-126">Kaynak sağlayıcıları, uygulamanız için kaynakları sağlayan hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="69457-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="69457-127">Sağlayıcısı sunar Azure kaynak dağıtabilmeniz için önce sağlayıcı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="69457-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="69457-128">Aşağıdaki komutu çalıştırarak IOT-örnekte, Batı ABD bölgesi adlı bir kaynak grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="69457-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="69457-129">`westus`kaynak grubu oluşturma konumdur.</span><span class="sxs-lookup"><span data-stu-id="69457-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="69457-130">Başka bir konuma kullanmak istiyorsanız, çalıştırabilirsiniz `az account list-locations -o table` tüm konumları Azure destekler.</span><span class="sxs-lookup"><span data-stu-id="69457-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="69457-131">IOT hub'ı, aşağıdaki komutu çalıştırarak IOT örnek kaynak grubunda oluşturun:</span><span class="sxs-lookup"><span data-stu-id="69457-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="69457-132">Varsayılan olarak, aracı, IOT hub'ı ücretsiz fiyatlandırma katmanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69457-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="69457-133">Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="69457-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="69457-134">IOT hub'ınızı adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="69457-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="69457-135">Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69457-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="69457-136">IOT hub'ınıza Edison'u kaydetme</span><span class="sxs-lookup"><span data-stu-id="69457-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="69457-137">IOT hub'ından ileti alıp IOT hub'ına iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="69457-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="69457-138">Edison'u IOT hub'ınıza çalışan aşağıdaki komutla kaydedin:</span><span class="sxs-lookup"><span data-stu-id="69457-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="69457-139">Özet</span><span class="sxs-lookup"><span data-stu-id="69457-139">Summary</span></span>
<span data-ttu-id="69457-140">IOT hub'ı oluşturulur ve Edison'u cihaz kimliğiyle IOT hub'ınıza kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="69457-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="69457-141">IOT hub'ınıza Edison'u iletileri gönderme hakkında bilgi edinmek hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="69457-141">You're ready to learn how to send messages from Edison to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69457-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="69457-142">Next steps</span></span>
<span data-ttu-id="69457-143">[Bir Azure işlevi uygulama ve işlemek ve IOT hub iletileri depolamak için bir Azure depolama hesabı oluştur][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="69457-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md