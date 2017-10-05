---
title: "Azure IOT - Ders 2 Arduino bağlanın: kayıt cihazı | Microsoft Docs"
description: "Bir kaynak grubu oluşturmak, Azure IOT hub oluşturma ve Azure CLI kullanarak Azure IOT hub'ı Adafruit yumuşatma M0 WiFi kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino bağlanma bulut, azure IOT hub, bulut, azure IOT hub'ı şeyler Internet aygıt, arduino bulut oluşturma"
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
ms.openlocfilehash: c5ad5e900671c7cedd3cdad2c2aa345315de223b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a><span data-ttu-id="7bdfe-104">IOT hub'ınızı oluşturun ve Adafruit yumuşatma M0 WiFi Arduino panonuzu kaydedin</span><span class="sxs-lookup"><span data-stu-id="7bdfe-104">Create your IoT hub and register your Adafruit Feather M0 WiFi Arduino board</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7bdfe-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="7bdfe-105">What you will do</span></span>
* <span data-ttu-id="7bdfe-106">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-106">Create a resource group.</span></span>
* <span data-ttu-id="7bdfe-107">Azure IOT hub'ınızdaki kaynak grubunu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="7bdfe-108">Arduino panonuzu Azure komut satırı arabirimi (Azure CLI) kullanarak Azure IOT hub'ına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-108">Add your Arduino board to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="7bdfe-109">IOT hub'ınıza Arduino panonuzu eklemek için Azure CLI kullandığınızda, hizmet Arduino panonuzu hizmeti ile kimlik doğrulaması için bir anahtar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-109">When you use the Azure CLI to add your Arduino board to your IoT hub, the service generates a key for your Arduino board to authenticate with the service.</span></span> <span data-ttu-id="7bdfe-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshoot].</span><span class="sxs-lookup"><span data-stu-id="7bdfe-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshoot].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7bdfe-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="7bdfe-111">What you will learn</span></span>
<span data-ttu-id="7bdfe-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="7bdfe-112">In this article, you will learn:</span></span>
* <span data-ttu-id="7bdfe-113">IOT hub'ı oluşturmak için Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="7bdfe-113">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="7bdfe-114">IOT hub'ınıza Arduino panonuz için bir cihaz kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="7bdfe-114">How to create a device identity for your Arduino board in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7bdfe-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="7bdfe-115">What you need</span></span>
* <span data-ttu-id="7bdfe-116">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="7bdfe-116">An Azure account</span></span>
* <span data-ttu-id="7bdfe-117">Azure CLI'ın yüklü olan bir bilgisayar</span><span class="sxs-lookup"><span data-stu-id="7bdfe-117">A computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="7bdfe-118">IOT hub'ınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7bdfe-118">Create your IoT hub</span></span>
<span data-ttu-id="7bdfe-119">Azure IOT Hub bağlanmak, izlemek ve milyonlarca IOT varlıklarını yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="7bdfe-120">IOT hub'ınızı oluşturması için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7bdfe-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="7bdfe-121">Aşağıdaki komutu çalıştırarak Azure hesabınızda oturum açın:</span><span class="sxs-lookup"><span data-stu-id="7bdfe-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="7bdfe-122">Kullanılabilir aboneliklerin bir başarılı oturum açma işleminden sonra listelenir.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="7bdfe-123">Aşağıdaki komutu çalıştırarak kullanmak istediğiniz varsayılan abonelik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="7bdfe-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="7bdfe-124">`subscription ID or name`çıktısında bulunabilir `az login` veya `az account list` komutu.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="7bdfe-125">Aşağıdaki komutu çalıştırarak sağlayıcıyı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-125">Register the provider by running the following command.</span></span> <span data-ttu-id="7bdfe-126">Kaynak sağlayıcıları, uygulamanız için kaynakları sağlayan hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="7bdfe-127">Sağlayıcısı sunar Azure kaynak dağıtabilmeniz için önce sağlayıcı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="7bdfe-128">Aşağıdaki komutu çalıştırarak IOT-örnekte, Batı ABD bölgesi adlı bir kaynak grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7bdfe-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="7bdfe-129">`westus`kaynak grubu oluşturma konumdur.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="7bdfe-130">Başka bir konuma kullanmak istiyorsanız, çalıştırabilirsiniz `az account list-locations -o table` tüm konumları Azure destekler.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="7bdfe-131">IOT hub'ı, aşağıdaki komutu çalıştırarak IOT örnek kaynak grubunda oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7bdfe-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="7bdfe-132">Varsayılan olarak, aracı, IOT hub'ı ücretsiz fiyatlandırma katmanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="7bdfe-133">Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="7bdfe-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="7bdfe-134">IOT hub'ınızı adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="7bdfe-135">Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-your-arduino-board-in-your-iot-hub"></a><span data-ttu-id="7bdfe-136">IOT hub'ınıza Arduino panonuzu kaydetme</span><span class="sxs-lookup"><span data-stu-id="7bdfe-136">Register your Arduino board in your IoT hub</span></span>
<span data-ttu-id="7bdfe-137">IOT hub'ından ileti alıp IOT hub'ına iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="7bdfe-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="7bdfe-138">Arduino panonuzu çalışan aşağıdaki komutu tarafından IOT hub'ınıza kaydedin:</span><span class="sxs-lookup"><span data-stu-id="7bdfe-138">Register your Arduino board in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="7bdfe-139">Özet</span><span class="sxs-lookup"><span data-stu-id="7bdfe-139">Summary</span></span>
<span data-ttu-id="7bdfe-140">IOT hub'ı oluşturulur ve Arduino panonuzu cihaz kimliğiyle IOT hub'ınıza kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-140">You've created an IoT hub and registered your Arduino board with a device identity in your IoT hub.</span></span> <span data-ttu-id="7bdfe-141">IOT hub'ınıza Arduino panonuzu iletileri gönderme hakkında bilgi edinmek hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="7bdfe-141">You're ready to learn how to send messages from your Arduino board to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bdfe-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7bdfe-142">Next steps</span></span>
<span data-ttu-id="7bdfe-143">[Bir Azure işlevi uygulama ve işlemek ve IOT hub iletileri depolamak için bir Azure depolama hesabı oluştur][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="7bdfe-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md