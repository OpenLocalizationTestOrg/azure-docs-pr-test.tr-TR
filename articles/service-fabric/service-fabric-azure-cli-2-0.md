---
title: "Azure Service Fabric ve Azure CLI 2.0 ile aaaGet başlatıldı"
description: "Azure CLI, sürüm 2.0 modülünde toouse hello Azure Service Fabric nasıl komutları öğrenin. Bilgi nasıl tooconnect tooa küme ve nasıl toomanage uygulamalar."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="7c041-104">Azure Service Fabric ve Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7c041-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="7c041-105">Azure Service Fabric kümeleri yönetmek komutları toohelp Hello Azure komut satırı aracı (Azure CLI) sürüm 2.0 içerir.</span><span class="sxs-lookup"><span data-stu-id="7c041-105">hello Azure command-line tool (Azure CLI) version 2.0 includes commands toohelp you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="7c041-106">Tooget Azure CLI ve Service Fabric ile çalışmaya nasıl öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7c041-106">Learn how tooget started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="7c041-107">Azure CLI 2.0’ı yükleme</span><span class="sxs-lookup"><span data-stu-id="7c041-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="7c041-108">Azure CLI 2.0 komutları toointeract ile kullanın ve Service Fabric kümeleri yönetin.</span><span class="sxs-lookup"><span data-stu-id="7c041-108">You can use Azure CLI 2.0 commands toointeract with and manage Service Fabric clusters.</span></span> <span data-ttu-id="7c041-109">tooget hello en son sürümünü Azure CLI, izleme hello [Azure CLI 2.0 Standart yükleme işlemi](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7c041-109">tooget hello latest version of Azure CLI, follow hello [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="7c041-110">Daha fazla bilgi için bkz: Merhaba [Azure CLI 2.0 genel bakış](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c041-110">For more information, see hello [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="7c041-111">Azure CLI söz dizimi</span><span class="sxs-lookup"><span data-stu-id="7c041-111">Azure CLI syntax</span></span>

<span data-ttu-id="7c041-112">Azure CLI'de, tüm Service Fabric komutlarının `az sf` ön eki vardır.</span><span class="sxs-lookup"><span data-stu-id="7c041-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="7c041-113">Kullanabileceğiniz hello komutlar hakkında genel bilgi için kullanmak `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="7c041-113">For general information about hello commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="7c041-114">Tek bir komutla ilgili yardım için, `az sf <command> -h` kullanın.</span><span class="sxs-lookup"><span data-stu-id="7c041-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="7c041-115">Azure CLI’de Service Fabric komutları şu adlandırma desenini izler:</span><span class="sxs-lookup"><span data-stu-id="7c041-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="7c041-116">`<object>`Merhaba hedefidir `<action>`.</span><span class="sxs-lookup"><span data-stu-id="7c041-116">`<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="7c041-117">Küme seçme</span><span class="sxs-lookup"><span data-stu-id="7c041-117">Select a cluster</span></span>

<span data-ttu-id="7c041-118">Herhangi bir işlem gerçekleştirmeden önce bir küme tooconnect seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c041-118">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="7c041-119">Örneğin, kod aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="7c041-119">For an example, see hello following code.</span></span> <span data-ttu-id="7c041-120">Merhaba kod tooan güvenli olmayan küme bağlanır.</span><span class="sxs-lookup"><span data-stu-id="7c041-120">hello code connects tooan unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="7c041-121">Üretim ortamında güvenli olmayan Service Fabric kümelerini kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7c041-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="7c041-122">Merhaba küme uç noktası öneki, olarak `http` veya `https`.</span><span class="sxs-lookup"><span data-stu-id="7c041-122">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="7c041-123">Merhaba HTTP ağ geçidi için başlangıç bağlantı noktası içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c041-123">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="7c041-124">Merhaba bağlantı noktasının ve adres olan hello Service Fabric Explorer URL hello gibi aynı.</span><span class="sxs-lookup"><span data-stu-id="7c041-124">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="7c041-125">Sertifikayla güvenliği sağlanan kümelerde, şifrelenmemiş .pem dosyaları veya .crt ve .key dosyaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c041-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="7c041-126">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7c041-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="7c041-127">Daha fazla bilgi için bkz: [Bağlan tooa güvenli Azure Service Fabric kümesi](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="7c041-127">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7c041-128">Merhaba `select` komutu, döndürmeden önce tüm istekler için hareket değil.</span><span class="sxs-lookup"><span data-stu-id="7c041-128">hello `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="7c041-129">bir küme doğru şekilde, belirttiğiniz tooverify gibi bir komut kullanın `az sf cluster health`.</span><span class="sxs-lookup"><span data-stu-id="7c041-129">tooverify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="7c041-130">Merhaba komutu herhangi bir hata döndürmez doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7c041-130">Verify that hello command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="7c041-131">Temel işlemler</span><span class="sxs-lookup"><span data-stu-id="7c041-131">Basic operations</span></span>

<span data-ttu-id="7c041-132">Küme bağlantı bilgileri birden çok Azure CLI oturumu arasında kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="7c041-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="7c041-133">Service Fabric kümesi seçtikten sonra hello kümede herhangi bir Service Fabric komutunu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c041-133">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="7c041-134">Örneğin, tooget hello Service Fabric kümesi sistem durumu, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="7c041-134">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="7c041-135">Merhaba komutu (JSON çıktısını hello Azure CLI yapılandırmasında belirtilen varsayılarak) çıktı hello aşağıdaki sonuçlanır:</span><span class="sxs-lookup"><span data-stu-id="7c041-135">hello command results in hello following output (assuming that JSON output is specified in hello Azure CLI configuration):</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="7c041-136">İpuçları ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="7c041-136">Tips and troubleshooting</span></span>

<span data-ttu-id="7c041-137">Hello Azure CLI Service Fabric komutları kullanırken sorunla çalıştırırsanız aşağıdaki bilgilerle yararlı bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c041-137">You might find hello following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="7c041-138">Bir sertifika PFX tooPEM biçiminden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="7c041-138">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="7c041-139">Azure CLI de PEM (.pem uzantısı) dosyaları gibi istemci tarafı sertifikalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="7c041-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="7c041-140">Windows'dan PFX dosyaları kullanırsanız, bu sertifikalar tooPEM biçime dönüştürmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c041-140">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="7c041-141">tooconvert bir PFX dosyası tooa PEM dosyası hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7c041-141">tooconvert a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="7c041-142">Daha fazla bilgi için bkz: Merhaba [OpenSSL belgelerine](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="7c041-142">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="7c041-143">Bağlantı sorunları</span><span class="sxs-lookup"><span data-stu-id="7c041-143">Connection issues</span></span>

<span data-ttu-id="7c041-144">Bazı işlemler iletiden hello oluşturabilir:</span><span class="sxs-lookup"><span data-stu-id="7c041-144">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="7c041-145">Bu hello küme uç noktası kullanılabilir olduğunu ve dinleme belirtildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="7c041-145">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="7c041-146">Ayrıca, ana bilgisayar ve bağlantı noktası, Service Fabric Explorer UI şu adresten edinilebilir bu hello doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7c041-146">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="7c041-147">tooupdate hello uç noktası, kullanım `az sf cluster select`.</span><span class="sxs-lookup"><span data-stu-id="7c041-147">tooupdate hello endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="7c041-148">Ayrıntılı günlükler</span><span class="sxs-lookup"><span data-stu-id="7c041-148">Detailed logs</span></span>

<span data-ttu-id="7c041-149">Hata ayıkladığınız veya sorun bildirdiğiniz sırada ayrıntılı günlükler çoğunlukla yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="7c041-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="7c041-150">Azure CLI sunan bir genel `--debug` hello ayrıntı günlük dosyalarının artırır bayrağı.</span><span class="sxs-lookup"><span data-stu-id="7c041-150">Azure CLI offers a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="7c041-151">Komut yardımı ve söz dizimi</span><span class="sxs-lookup"><span data-stu-id="7c041-151">Command help and syntax</span></span>

<span data-ttu-id="7c041-152">Azure CLI ile aynı kuralları hello Service Fabric komutları izleyin.</span><span class="sxs-lookup"><span data-stu-id="7c041-152">Service Fabric commands follow hello same conventions as Azure CLI.</span></span> <span data-ttu-id="7c041-153">Belirli bir komut veya bir komut grubunu ile ilgili Yardım için hello kullanın `-h` bayrağı:</span><span class="sxs-lookup"><span data-stu-id="7c041-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="7c041-154">Bir örnek daha:</span><span class="sxs-lookup"><span data-stu-id="7c041-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
