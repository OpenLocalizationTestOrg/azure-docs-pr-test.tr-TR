---
title: "Intel Edison'u (düğüm) tooAzure IOT - Ders 2 bağlanın: kayıt cihazı | Microsoft Docs"
description: "Bir kaynak grubu oluşturmak, Azure IOT hub oluşturma ve Edison'u hello Azure IOT hub'hello Azure CLI kullanarak kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: c1465cc2-d0d9-4326-967c-64d95b61dd54
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a70cd8d6a6d620a2cf6226397e061af6cf81e0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="a8f34-103">IOT hub'ınızı oluşturun ve Intel Edison'u kaydedin</span><span class="sxs-lookup"><span data-stu-id="a8f34-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a8f34-104">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="a8f34-104">What you will do</span></span>
* <span data-ttu-id="a8f34-105">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8f34-105">Create a resource group.</span></span>
* <span data-ttu-id="a8f34-106">Azure IOT hub'ınızı hello kaynak grubunda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8f34-106">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="a8f34-107">Intel Edison'u toohello Azure IOT hub'hello Azure komut satırı arabirimi (Azure CLI) kullanarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8f34-107">Add Intel Edison toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="a8f34-108">Hello Azure CLI tooadd Edison'u tooyour IOT hub'ı kullandığınızda, hello hizmeti hello hizmetiyle Edison'u tooauthenticate için bir anahtar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a8f34-108">When you use hello Azure CLI tooadd Edison tooyour IoT hub, hello service generates a key for Edison tooauthenticate with hello service.</span></span> <span data-ttu-id="a8f34-109">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a8f34-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a8f34-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="a8f34-110">What you will learn</span></span>
<span data-ttu-id="a8f34-111">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="a8f34-111">In this article, you will learn:</span></span>
* <span data-ttu-id="a8f34-112">Nasıl toouse hello Azure CLI toocreate IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="a8f34-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="a8f34-113">Nasıl toocreate IOT hub'ınızdaki Edison'u için bir cihaz kimliği.</span><span class="sxs-lookup"><span data-stu-id="a8f34-113">How toocreate a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a8f34-114">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="a8f34-114">What you need</span></span>
* <span data-ttu-id="a8f34-115">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="a8f34-115">An Azure account.</span></span> <span data-ttu-id="a8f34-116">Bir Azure hesabınız yoksa, oluşturma bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="a8f34-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="a8f34-117">Hello Azure CLI yüklenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8f34-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="a8f34-118">IOT hub'ınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8f34-118">Create your IoT hub</span></span>
<span data-ttu-id="a8f34-119">Azure IOT Hub bağlanmak, izlemek ve milyonlarca IOT varlıklarını yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a8f34-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="a8f34-120">toocreate IOT hub'ınızı şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a8f34-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="a8f34-121">İçinde tooyour hello aşağıdaki komutu çalıştırarak Azure hesabı imzalayın:</span><span class="sxs-lookup"><span data-stu-id="a8f34-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="a8f34-122">Kullanılabilir aboneliklerin bir başarılı oturum açma işleminden sonra listelenir.</span><span class="sxs-lookup"><span data-stu-id="a8f34-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="a8f34-123">Merhaba aşağıdaki komutu çalıştırarak toouse istediğiniz hello varsayılan abonelik ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="a8f34-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="a8f34-124">`subscription ID or name`Merhaba Hello çıktısında bulunabilir `az login` veya hello `az account list` komutu.</span><span class="sxs-lookup"><span data-stu-id="a8f34-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="a8f34-125">Merhaba sağlayıcıyı hello aşağıdaki komutu çalıştırarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a8f34-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="a8f34-126">Kaynak sağlayıcıları, uygulamanız için kaynakları sağlayan hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="a8f34-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="a8f34-127">Merhaba sağlayıcısı teklifleri hello Azure kaynak dağıtmadan önce hello sağlayıcısı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8f34-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="a8f34-128">Adlı bir kaynak grubu hello Batı ABD bölgesinde hello aşağıdaki komutu çalıştırarak IOT örnek oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a8f34-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="a8f34-129">`westus`kaynak grubu oluşturma hello bir konumdur.</span><span class="sxs-lookup"><span data-stu-id="a8f34-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="a8f34-130">Başka bir konuma toouse istiyorsanız çalıştırabilirsiniz `az account list-locations -o table` toosee tüm hello konumları Azure destekler.</span><span class="sxs-lookup"><span data-stu-id="a8f34-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="a8f34-131">IOT hub'ı hello aşağıdaki komutu çalıştırarak hello IOT örnek kaynak grubunda oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a8f34-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="a8f34-132">Varsayılan olarak, hello aracı hello ücretsiz fiyatlandırma katmanında bir IOT hub'ı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a8f34-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="a8f34-133">Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="a8f34-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="a8f34-134">IOT hub'ınızı Hello adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8f34-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="a8f34-135">Azure aboneliğinizde Azure IOT hub'ı tek bir F1 sürümünü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8f34-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="a8f34-136">IOT hub'ınıza Edison'u kaydetme</span><span class="sxs-lookup"><span data-stu-id="a8f34-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="a8f34-137">IOT hub'ından ileti alıp tooyour IOT hub'ı iletileri gönderen her aygıt benzersiz bir kimlik ile kayıtlı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="a8f34-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="a8f34-138">Edison'u IOT hub'ınıza çalışan aşağıdaki komutla kaydedin:</span><span class="sxs-lookup"><span data-stu-id="a8f34-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="a8f34-139">Özet</span><span class="sxs-lookup"><span data-stu-id="a8f34-139">Summary</span></span>
<span data-ttu-id="a8f34-140">IOT hub'ı oluşturulur ve Edison'u cihaz kimliğiyle IOT hub'ınıza kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="a8f34-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="a8f34-141">Nasıl toosend Edison'u tooyour IOT hub'ından iletileri hazır toolearn demektir.</span><span class="sxs-lookup"><span data-stu-id="a8f34-141">You're ready toolearn how toosend messages from Edison tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8f34-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8f34-142">Next steps</span></span>
<span data-ttu-id="a8f34-143">[Bir Azure işlevi uygulama ve Azure Storage hesabı tooprocess ve deposu IOT hub'ı iletileri oluşturmak][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="a8f34-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md