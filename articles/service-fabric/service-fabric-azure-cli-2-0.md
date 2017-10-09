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
# <a name="azure-service-fabric-and-azure-cli-20"></a>Azure Service Fabric ve Azure CLI 2.0

Azure Service Fabric kümeleri yönetmek komutları toohelp Hello Azure komut satırı aracı (Azure CLI) sürüm 2.0 içerir. Tooget Azure CLI ve Service Fabric ile çalışmaya nasıl öğrenin.

## <a name="install-azure-cli-20"></a>Azure CLI 2.0’ı yükleme

Azure CLI 2.0 komutları toointeract ile kullanın ve Service Fabric kümeleri yönetin. tooget hello en son sürümünü Azure CLI, izleme hello [Azure CLI 2.0 Standart yükleme işlemi](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

Daha fazla bilgi için bkz: Merhaba [Azure CLI 2.0 genel bakış](https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="azure-cli-syntax"></a>Azure CLI söz dizimi

Azure CLI'de, tüm Service Fabric komutlarının `az sf` ön eki vardır. Kullanabileceğiniz hello komutlar hakkında genel bilgi için kullanmak `az sf -h`. Tek bir komutla ilgili yardım için, `az sf <command> -h` kullanın.

Azure CLI’de Service Fabric komutları şu adlandırma desenini izler:

```azurecli
az sf <object> <action>
```

`<object>`Merhaba hedefidir `<action>`.

## <a name="select-a-cluster"></a>Küme seçme

Herhangi bir işlem gerçekleştirmeden önce bir küme tooconnect seçmeniz gerekir. Örneğin, kod aşağıdaki hello bakın. Merhaba kod tooan güvenli olmayan küme bağlanır.

> [!WARNING]
> Üretim ortamında güvenli olmayan Service Fabric kümelerini kullanmayın.

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

Merhaba küme uç noktası öneki, olarak `http` veya `https`. Merhaba HTTP ağ geçidi için başlangıç bağlantı noktası içermesi gerekir. Merhaba bağlantı noktasının ve adres olan hello Service Fabric Explorer URL hello gibi aynı.

Sertifikayla güvenliği sağlanan kümelerde, şifrelenmemiş .pem dosyaları veya .crt ve .key dosyaları kullanabilirsiniz. Örneğin:

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Daha fazla bilgi için bkz: [Bağlan tooa güvenli Azure Service Fabric kümesi](service-fabric-connect-to-secure-cluster.md).

> [!NOTE]
> Merhaba `select` komutu, döndürmeden önce tüm istekler için hareket değil. bir küme doğru şekilde, belirttiğiniz tooverify gibi bir komut kullanın `az sf cluster health`. Merhaba komutu herhangi bir hata döndürmez doğrulayın.

## <a name="basic-operations"></a>Temel işlemler

Küme bağlantı bilgileri birden çok Azure CLI oturumu arasında kalıcıdır. Service Fabric kümesi seçtikten sonra hello kümede herhangi bir Service Fabric komutunu çalıştırabilirsiniz.

Örneğin, tooget hello Service Fabric kümesi sistem durumu, komutu aşağıdaki hello kullan:

```azurecli
az sf cluster health
```

Merhaba komutu (JSON çıktısını hello Azure CLI yapılandırmasında belirtilen varsayılarak) çıktı hello aşağıdaki sonuçlanır:

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

## <a name="tips-and-troubleshooting"></a>İpuçları ve sorun giderme

Hello Azure CLI Service Fabric komutları kullanırken sorunla çalıştırırsanız aşağıdaki bilgilerle yararlı bulabilirsiniz.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Bir sertifika PFX tooPEM biçiminden Dönüştür

Azure CLI de PEM (.pem uzantısı) dosyaları gibi istemci tarafı sertifikalarını destekler. Windows'dan PFX dosyaları kullanırsanız, bu sertifikalar tooPEM biçime dönüştürmesi gerekir. tooconvert bir PFX dosyası tooa PEM dosyası hello aşağıdaki komutu kullanın:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Daha fazla bilgi için bkz: Merhaba [OpenSSL belgelerine](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Bağlantı sorunları

Bazı işlemler iletiden hello oluşturabilir:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Bu hello küme uç noktası kullanılabilir olduğunu ve dinleme belirtildiğinden emin olun. Ayrıca, ana bilgisayar ve bağlantı noktası, Service Fabric Explorer UI şu adresten edinilebilir bu hello doğrulayın. tooupdate hello uç noktası, kullanım `az sf cluster select`.

### <a name="detailed-logs"></a>Ayrıntılı günlükler

Hata ayıkladığınız veya sorun bildirdiğiniz sırada ayrıntılı günlükler çoğunlukla yararlı olur. Azure CLI sunan bir genel `--debug` hello ayrıntı günlük dosyalarının artırır bayrağı.

### <a name="command-help-and-syntax"></a>Komut yardımı ve söz dizimi

Azure CLI ile aynı kuralları hello Service Fabric komutları izleyin. Belirli bir komut veya bir komut grubunu ile ilgili Yardım için hello kullanın `-h` bayrağı:

```azurecli
az sf application -h
```

Bir örnek daha:

```azurecli
az sf application create -h
```
