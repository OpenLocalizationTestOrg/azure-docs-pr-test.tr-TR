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
# <a name="azure-service-fabric-command-line"></a>Azure Service Fabric komut satırı

Hello Azure Service Fabric CLI (sfctl) etkileşim ve Azure Service Fabric varlıklar yönetmek için bir komut satırı yardımcı programıdır. Sfctl, Windows veya Linux kümeleriyle kullanılabilir. Sfctl python’ın desteklendiği tüm platformlarda çalışır.

## <a name="prerequisites"></a>Ön koşullar

Önceki tooinstallation ortamınız, python ve PIP yüklü olduğundan emin olun. Daha fazla bilgi için hello bakalım [PIP hızlı başlangıç belgelerine](https://pip.pypa.io/en/latest/quickstart/)ve resmi [python yüklemek belgelerine](https://wiki.python.org/moin/BeginnersGuide/Download).

Her iki python 2.7 ve 3.6 destekleniyorsa toouse python 3.6 önerilir.

## <a name="install"></a>Yükleme

Hello Azure Service Fabric CLI (sfctl) python paket olarak bulunmaktadır. çalıştırma tooinstall hello en son sürümü:

```bash
pip install sfctl
```

Yüklendikten sonra Çalıştır `sfctl -h` kullanılabilir komutlar hakkında tooget bilgi.

## <a name="cli-syntax"></a>CLI söz dizimi

Komutlarda her zaman `sfctl` ön eki bulunur. Kullanabileceğiniz tüm komutlarla ilgili genel bilgi için, `sfctl -h` kullanın. Tek bir komutla ilgili yardım için, `sfctl <command> -h` kullanın.

Komutları izleyin hello hello hedefi ile tekrarlanabilir bir yapı komut önceki hello fiil veya eylem:

```azurecli
sfctl <object> <action>
```

Bu örnekte, `<object>` hello hedefidir `<action>`.

## <a name="select-a-cluster"></a>Küme seçme

Herhangi bir işlem gerçekleştirmeden önce bir küme tooconnect seçmeniz gerekir. Örneğin, tooselect aşağıdaki hello çalıştırabilir ve toohello küme hello adı ile bağlanma `testcluster.com`.

> [!WARNING]
> Üretim ortamında güvenli olmayan Service Fabric kümelerini kullanmayın.

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

Merhaba küme uç noktası öneki, olarak `http` veya `https`. Merhaba HTTP ağ geçidi için başlangıç bağlantı noktası içermesi gerekir. Merhaba bağlantı noktasının ve adres olan hello Service Fabric Explorer URL hello gibi aynı.

Güvenliği bir sertifika ile sağlanan kümeler için PEM kodlu bir sertifika belirtebilirsiniz. Merhaba sertifika tek bir dosya veya sertifika ve anahtar çifti belirtilebilir.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Daha fazla bilgi için bkz: [Bağlan tooa güvenli Azure Service Fabric kümesi](service-fabric-connect-to-secure-cluster.md).

## <a name="basic-operations"></a>Temel işlemler

Küme bağlantı bilgileri birden çok sfctl oturumu arasında kalıcıdır. Service Fabric kümesi seçtikten sonra hello kümede herhangi bir Service Fabric komutunu çalıştırabilirsiniz.

Örneğin, tooget hello Service Fabric kümesi sistem durumu, komutu aşağıdaki hello kullan:

```azurecli
sfctl cluster health
```

Çıktı aşağıdaki hello Hello komutu sonuçları:

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

Bazı öneriler ve sık karşılaşılan sorunları çözmek için ipuçları.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Bir sertifika PFX tooPEM biçiminden Dönüştür

Merhaba Service Fabric CLI PEM (.pem uzantılı) dosyaları olarak istemci tarafı sertifikalar destekler. Windows'dan PFX dosyaları kullanırsanız, bu sertifikalar tooPEM biçime dönüştürmesi gerekir. tooconvert bir PFX dosyası tooa PEM dosyasını aşağıdaki komutu kullanın:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Daha fazla bilgi için bkz: Merhaba [OpenSSL belgelerine](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Bağlantı sorunları

Bazı işlemler iletiden hello oluşturabilir:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Bu hello küme uç noktası kullanılabilir olduğunu ve dinleme belirtildiğinden emin olun. Ayrıca, ana bilgisayar ve bağlantı noktası, Service Fabric Explorer UI şu adresten edinilebilir bu hello doğrulayın. tooupdate hello uç noktası, kullanım `sfctl cluster select`.

### <a name="detailed-logs"></a>Ayrıntılı günlükler

Hata ayıkladığınız veya sorun bildirdiğiniz sırada ayrıntılı günlükler çoğunlukla yararlı olur. Var olan bir genel `--debug` hello ayrıntı günlük dosyalarının artırır bayrağı.

### <a name="command-help-and-syntax"></a>Komut yardımı ve söz dizimi

Belirli bir komut veya bir komut grubunu ile ilgili Yardım için hello kullanın `-h` bayrağı:

```azurecli
sfctl application -h
```

Bir örnek daha:

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a>Sonraki adımlar

* [Bir uygulama hello Azure Service Fabric CLI oluşturup dağıtın](service-fabric-application-lifecycle-sfctl.md)
* [Linux’ta Service Fabric kullanmaya başlama](service-fabric-get-started-linux.md)
