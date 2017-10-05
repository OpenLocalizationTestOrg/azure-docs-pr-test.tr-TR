---
title: "Azure Service Fabric ve Azure CLI 2.0 ile çalışmaya başlama"
description: "Azure CLI, sürüm 2.0'da Azure Service Fabric komutları modülünü kullanmayı öğrenin. Kümeye bağlanmayı ve uygulamaları yönetmeyi öğrenin."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ee3302b984ca2f5509755dc17b0a5fd06ace0afe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="fe3a8-104">Azure Service Fabric ve Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fe3a8-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="fe3a8-105">Azure komut satırı aracı (Azure CLI) sürüm 2.0, Azure Service Fabric kümelerini yönetmenize yardımcı olan komutlar içerir.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-105">The Azure command-line tool (Azure CLI) version 2.0 includes commands to help you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="fe3a8-106">Azure CLI ve Service Fabric ile çalışmaya başlamayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-106">Learn how to get started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="fe3a8-107">Azure CLI 2.0’ı yükleme</span><span class="sxs-lookup"><span data-stu-id="fe3a8-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="fe3a8-108">Azure CLI 2.0 komutlarını kullanarak Service Fabric kümeleriyle etkileşim kurabilir ve bu kümeleri yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-108">You can use Azure CLI 2.0 commands to interact with and manage Service Fabric clusters.</span></span> <span data-ttu-id="fe3a8-109">Azure CLI'nin en son sürümünü almak için [Azure CLI 2.0 standart yükleme işlemini](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) izleyin.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-109">To get the latest version of Azure CLI, follow the [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="fe3a8-110">Daha fazla bilgi için bkz. [Azure CLI 2.0 aracına genel bakış](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fe3a8-110">For more information, see the [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="fe3a8-111">Azure CLI söz dizimi</span><span class="sxs-lookup"><span data-stu-id="fe3a8-111">Azure CLI syntax</span></span>

<span data-ttu-id="fe3a8-112">Azure CLI'de, tüm Service Fabric komutlarının `az sf` ön eki vardır.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="fe3a8-113">Kullanabileceğiniz komutlarla ilgili genel bilgi için, `az sf -h` kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-113">For general information about the commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="fe3a8-114">Tek bir komutla ilgili yardım için, `az sf <command> -h` kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="fe3a8-115">Azure CLI’de Service Fabric komutları şu adlandırma desenini izler:</span><span class="sxs-lookup"><span data-stu-id="fe3a8-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="fe3a8-116">`<object>`, `<action>` hedefidir.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-116">`<object>` is the target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="fe3a8-117">Küme seçme</span><span class="sxs-lookup"><span data-stu-id="fe3a8-117">Select a cluster</span></span>

<span data-ttu-id="fe3a8-118">Herhangi bir işlem gerçekleştirmeden önce bağlantı kurulacak bir küme seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-118">Before you perform any operations, you must select a cluster to connect to.</span></span> <span data-ttu-id="fe3a8-119">Örneğin, aşağıdaki kodu bakın.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-119">For an example, see the following code.</span></span> <span data-ttu-id="fe3a8-120">Kod güvenli olmayan bir kümeye bağlanır.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-120">The code connects to an unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="fe3a8-121">Üretim ortamında güvenli olmayan Service Fabric kümelerini kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="fe3a8-122">Küme uç noktasının `http` veya `https` ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-122">The cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="fe3a8-123">HTTP ağ geçidi için bağlantı noktasını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-123">It must include the port for the HTTP gateway.</span></span> <span data-ttu-id="fe3a8-124">Bağlantı noktası ve adres, Service Fabric Explorer URL'si ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-124">The port and address are the same as the Service Fabric Explorer URL.</span></span>

<span data-ttu-id="fe3a8-125">Sertifikayla güvenliği sağlanan kümelerde, şifrelenmemiş .pem dosyaları veya .crt ve .key dosyaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="fe3a8-126">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fe3a8-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="fe3a8-127">Daha fazla bilgi için bkz. [Güvenli Azure Service Fabric kümesine bağlanma](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="fe3a8-127">For more information, see [Connect to a secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fe3a8-128">`select` komutu, döndürülmeden önce hiçbir istek üzerinde işlem yapmaz.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-128">The `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="fe3a8-129">Kümeyi doğru belirttiğinizden emin olmak için, `az sf cluster health` gibi bir komut kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-129">To verify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="fe3a8-130">Komutun herhangi bir hata döndürmediğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-130">Verify that the command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="fe3a8-131">Temel işlemler</span><span class="sxs-lookup"><span data-stu-id="fe3a8-131">Basic operations</span></span>

<span data-ttu-id="fe3a8-132">Küme bağlantı bilgileri birden çok Azure CLI oturumu arasında kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="fe3a8-133">Service Fabric kümesini seçtikten sonra, kümede tüm Service Fabric komutlarını çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-133">After you select a Service Fabric cluster, you can run any Service Fabric command on the cluster.</span></span>

<span data-ttu-id="fe3a8-134">Örneğin, Service Fabric kümesinin sistem durumunu almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="fe3a8-134">For example, to get the Service Fabric cluster health state, use the following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="fe3a8-135">Komut sonuçta şu çıkışı oluşturur (JSON çıkışının Azure CLI yapılandırmasında belirtildiği varsayılarak):</span><span class="sxs-lookup"><span data-stu-id="fe3a8-135">The command results in the following output (assuming that JSON output is specified in the Azure CLI configuration):</span></span>

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="fe3a8-136">İpuçları ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="fe3a8-136">Tips and troubleshooting</span></span>

<span data-ttu-id="fe3a8-137">Azure CLI'de Service Fabric komutlarını kullanırken sorunlarla karşılaşıyorsanız, aşağıdaki bilgileri yararlı bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-137">You might find the following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a><span data-ttu-id="fe3a8-138">Sertifikayı PFX’ten PEM biçimine dönüştürme</span><span class="sxs-lookup"><span data-stu-id="fe3a8-138">Convert a certificate from PFX to PEM format</span></span>

<span data-ttu-id="fe3a8-139">Azure CLI de PEM (.pem uzantısı) dosyaları gibi istemci tarafı sertifikalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="fe3a8-140">Windows'dan PFX dosyalarını kullanıyorsanız, söz konusu sertifikaları PEM biçimine dönüştürmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-140">If you use PFX files from Windows, you must convert those certificates to PEM format.</span></span> <span data-ttu-id="fe3a8-141">PFX dosyasını PEM dosyasına dönüştürmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="fe3a8-141">To convert a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="fe3a8-142">Daha fazla bilgi için bkz. [OpenSSL belgeleri](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="fe3a8-142">For more information, see the [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="fe3a8-143">Bağlantı sorunları</span><span class="sxs-lookup"><span data-stu-id="fe3a8-143">Connection issues</span></span>

<span data-ttu-id="fe3a8-144">Bazı işlemler aşağıdaki iletiyi oluşturabilir:</span><span class="sxs-lookup"><span data-stu-id="fe3a8-144">Some operations might generate the following message:</span></span>

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="fe3a8-145">Belirtilen küme uç noktasının kullanılabilir olduğunu ve dinlediğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-145">Verify that the specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="fe3a8-146">Ayrıca söz konusu konakta ve bağlantı noktasında Service Fabric Explorer Kullanıcı Arabiriminin kullanılabilir olduğunu da doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-146">Also, verify that the Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="fe3a8-147">Uç noktayı güncelleştirmek için `az sf cluster select` kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-147">To update the endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="fe3a8-148">Ayrıntılı günlükler</span><span class="sxs-lookup"><span data-stu-id="fe3a8-148">Detailed logs</span></span>

<span data-ttu-id="fe3a8-149">Hata ayıkladığınız veya sorun bildirdiğiniz sırada ayrıntılı günlükler çoğunlukla yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="fe3a8-150">Azure CLI, günlük dosyalarının ayrıntı düzeyini artıran genel bir `--debug` bayrağı sunar.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-150">Azure CLI offers a global `--debug` flag that increases the verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="fe3a8-151">Komut yardımı ve söz dizimi</span><span class="sxs-lookup"><span data-stu-id="fe3a8-151">Command help and syntax</span></span>

<span data-ttu-id="fe3a8-152">Service Fabric komutları, Azure CLI ile aynı kuralları izler.</span><span class="sxs-lookup"><span data-stu-id="fe3a8-152">Service Fabric commands follow the same conventions as Azure CLI.</span></span> <span data-ttu-id="fe3a8-153">Belirli bir komut veya komut grubuyla ilgili yardım almak için `-h` bayrağını kullanın:</span><span class="sxs-lookup"><span data-stu-id="fe3a8-153">For help with a specific command or a group of commands, use the `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="fe3a8-154">Bir örnek daha:</span><span class="sxs-lookup"><span data-stu-id="fe3a8-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
