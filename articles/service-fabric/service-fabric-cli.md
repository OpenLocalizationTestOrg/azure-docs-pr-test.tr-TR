---
title: "Azure Service Fabric CLI (sfctl) aaaGet başlatıldı"
description: "Nasıl toouse hello Azure Service Fabric CLI öğrenin. Bilgi nasıl tooconnect tooa küme ve nasıl toomanage uygulamalar."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="9c552-104">Azure Service Fabric komut satırı</span><span class="sxs-lookup"><span data-stu-id="9c552-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="9c552-105">Hello Azure Service Fabric CLI (sfctl) etkileşim ve Azure Service Fabric varlıklar yönetmek için bir komut satırı yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="9c552-105">hello Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="9c552-106">Sfctl, Windows veya Linux kümeleriyle kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9c552-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="9c552-107">Sfctl python’ın desteklendiği tüm platformlarda çalışır.</span><span class="sxs-lookup"><span data-stu-id="9c552-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c552-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9c552-108">Prerequisites</span></span>

<span data-ttu-id="9c552-109">Önceki tooinstallation ortamınız, python ve PIP yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9c552-109">Prior tooinstallation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="9c552-110">Daha fazla bilgi için hello bakalım [PIP hızlı başlangıç belgelerine](https://pip.pypa.io/en/latest/quickstart/)ve resmi [python yüklemek belgelerine](https://wiki.python.org/moin/BeginnersGuide/Download).</span><span class="sxs-lookup"><span data-stu-id="9c552-110">For more information, take a look at hello [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="9c552-111">Her iki python 2.7 ve 3.6 destekleniyorsa toouse python 3.6 önerilir.</span><span class="sxs-lookup"><span data-stu-id="9c552-111">While both python 2.7 and 3.6 are supported, it is recommended toouse python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="9c552-112">Yükleme</span><span class="sxs-lookup"><span data-stu-id="9c552-112">Install</span></span>

<span data-ttu-id="9c552-113">Hello Azure Service Fabric CLI (sfctl) python paket olarak bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9c552-113">hello Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="9c552-114">çalıştırma tooinstall hello en son sürümü:</span><span class="sxs-lookup"><span data-stu-id="9c552-114">tooinstall hello latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="9c552-115">Yüklendikten sonra Çalıştır `sfctl -h` kullanılabilir komutlar hakkında tooget bilgi.</span><span class="sxs-lookup"><span data-stu-id="9c552-115">After installation, run `sfctl -h` tooget information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="9c552-116">CLI söz dizimi</span><span class="sxs-lookup"><span data-stu-id="9c552-116">CLI syntax</span></span>

<span data-ttu-id="9c552-117">Komutlarda her zaman `sfctl` ön eki bulunur.</span><span class="sxs-lookup"><span data-stu-id="9c552-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="9c552-118">Kullanabileceğiniz tüm komutlarla ilgili genel bilgi için, `sfctl -h` kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c552-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="9c552-119">Tek bir komutla ilgili yardım için, `sfctl <command> -h` kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c552-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="9c552-120">Komutları izleyin hello hello hedefi ile tekrarlanabilir bir yapı komut önceki hello fiil veya eylem:</span><span class="sxs-lookup"><span data-stu-id="9c552-120">Commands follow a repeatable structure, with hello target of hello command preceding hello verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="9c552-121">Bu örnekte, `<object>` hello hedefidir `<action>`.</span><span class="sxs-lookup"><span data-stu-id="9c552-121">In this example, `<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="9c552-122">Küme seçme</span><span class="sxs-lookup"><span data-stu-id="9c552-122">Select a cluster</span></span>

<span data-ttu-id="9c552-123">Herhangi bir işlem gerçekleştirmeden önce bir küme tooconnect seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c552-123">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="9c552-124">Örneğin, tooselect aşağıdaki hello çalıştırabilir ve toohello küme hello adı ile bağlanma `testcluster.com`.</span><span class="sxs-lookup"><span data-stu-id="9c552-124">For example, run hello following tooselect and connect toohello cluster with hello name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="9c552-125">Üretim ortamında güvenli olmayan Service Fabric kümelerini kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="9c552-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="9c552-126">Merhaba küme uç noktası öneki, olarak `http` veya `https`.</span><span class="sxs-lookup"><span data-stu-id="9c552-126">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="9c552-127">Merhaba HTTP ağ geçidi için başlangıç bağlantı noktası içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c552-127">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="9c552-128">Merhaba bağlantı noktasının ve adres olan hello Service Fabric Explorer URL hello gibi aynı.</span><span class="sxs-lookup"><span data-stu-id="9c552-128">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="9c552-129">Güvenliği bir sertifika ile sağlanan kümeler için PEM kodlu bir sertifika belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c552-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="9c552-130">Merhaba sertifika tek bir dosya veya sertifika ve anahtar çifti belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="9c552-130">hello certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="9c552-131">Daha fazla bilgi için bkz: [Bağlan tooa güvenli Azure Service Fabric kümesi](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9c552-131">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="9c552-132">Temel işlemler</span><span class="sxs-lookup"><span data-stu-id="9c552-132">Basic operations</span></span>

<span data-ttu-id="9c552-133">Küme bağlantı bilgileri birden çok sfctl oturumu arasında kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="9c552-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="9c552-134">Service Fabric kümesi seçtikten sonra hello kümede herhangi bir Service Fabric komutunu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c552-134">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="9c552-135">Örneğin, tooget hello Service Fabric kümesi sistem durumu, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9c552-135">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="9c552-136">Çıktı aşağıdaki hello Hello komutu sonuçları:</span><span class="sxs-lookup"><span data-stu-id="9c552-136">hello command results in hello following output:</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="9c552-137">İpuçları ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="9c552-137">Tips and troubleshooting</span></span>

<span data-ttu-id="9c552-138">Bazı öneriler ve sık karşılaşılan sorunları çözmek için ipuçları.</span><span class="sxs-lookup"><span data-stu-id="9c552-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="9c552-139">Bir sertifika PFX tooPEM biçiminden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="9c552-139">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="9c552-140">Merhaba Service Fabric CLI PEM (.pem uzantılı) dosyaları olarak istemci tarafı sertifikalar destekler.</span><span class="sxs-lookup"><span data-stu-id="9c552-140">hello Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="9c552-141">Windows'dan PFX dosyaları kullanırsanız, bu sertifikalar tooPEM biçime dönüştürmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c552-141">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="9c552-142">tooconvert bir PFX dosyası tooa PEM dosyasını aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="9c552-142">tooconvert a PFX file tooa PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="9c552-143">Daha fazla bilgi için bkz: Merhaba [OpenSSL belgelerine](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="9c552-143">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="9c552-144">Bağlantı sorunları</span><span class="sxs-lookup"><span data-stu-id="9c552-144">Connection issues</span></span>

<span data-ttu-id="9c552-145">Bazı işlemler iletiden hello oluşturabilir:</span><span class="sxs-lookup"><span data-stu-id="9c552-145">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="9c552-146">Bu hello küme uç noktası kullanılabilir olduğunu ve dinleme belirtildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="9c552-146">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="9c552-147">Ayrıca, ana bilgisayar ve bağlantı noktası, Service Fabric Explorer UI şu adresten edinilebilir bu hello doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="9c552-147">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="9c552-148">tooupdate hello uç noktası, kullanım `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="9c552-148">tooupdate hello endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="9c552-149">Ayrıntılı günlükler</span><span class="sxs-lookup"><span data-stu-id="9c552-149">Detailed logs</span></span>

<span data-ttu-id="9c552-150">Hata ayıkladığınız veya sorun bildirdiğiniz sırada ayrıntılı günlükler çoğunlukla yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="9c552-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="9c552-151">Var olan bir genel `--debug` hello ayrıntı günlük dosyalarının artırır bayrağı.</span><span class="sxs-lookup"><span data-stu-id="9c552-151">There is a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="9c552-152">Komut yardımı ve söz dizimi</span><span class="sxs-lookup"><span data-stu-id="9c552-152">Command help and syntax</span></span>

<span data-ttu-id="9c552-153">Belirli bir komut veya bir komut grubunu ile ilgili Yardım için hello kullanın `-h` bayrağı:</span><span class="sxs-lookup"><span data-stu-id="9c552-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="9c552-154">Bir örnek daha:</span><span class="sxs-lookup"><span data-stu-id="9c552-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="9c552-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c552-155">Next steps</span></span>

* [<span data-ttu-id="9c552-156">Bir uygulama hello Azure Service Fabric CLI oluşturup dağıtın</span><span class="sxs-lookup"><span data-stu-id="9c552-156">Deploy an application with hello Azure Service Fabric CLI</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="9c552-157">Linux’ta Service Fabric kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9c552-157">Get started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
