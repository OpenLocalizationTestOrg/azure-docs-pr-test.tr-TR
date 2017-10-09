---
title: "aaaAdd ek Azure depolama hesapları tooHDInsight | Microsoft Docs"
description: "Nasıl tooan olan bir Hdınsight kümesine tooadd ek Azure depolama hesapları hakkında bilgi edinin."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a>Ek depolama hesapları tooHDInsight Ekle

Nasıl tooHDInsight toouse betik eylemleri tooadd ek Azure depolama hesapları hakkında bilgi edinin. Merhaba bu belgedeki adımlar bir depolama hesabı tooan varolan Linux tabanlı Hdınsight kümesi ekleyin.

> [!IMPORTANT]
> Merhaba bu belgedeki oluşturulduktan sonra ek depolama alanı tooa küme ekleme hakkında bilgilerdir. Küme oluşturma sırasında depolama hesapları ekleme hakkında daha fazla bilgi için bkz: [Hdınsight Hadoop, Spark, Kafka ve daha fazla ile kümelerde ayarlama](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="how-it-works"></a>Nasıl çalışır?

Bu komut dosyası şu parametreler hello alır:

* __Azure depolama hesabı adı__: hello depolama hesabı tooadd toohello Hdınsight kümesi hello adı. Hdınsight, Hello komut dosyasını çalıştırdıktan sonra okuma ve bu depolama hesabında depolanan verileri yazma.

* __Azure depolama hesabı anahtarı__: bir anahtar, veren erişim toohello depolama hesabı.

* __-p__ (isteğe bağlı): belirtilmişse hello anahtarı şifrelenmemiş ve düz metin olarak hello core-site.xml dosyasında depolanır.

İşleme sırasında hello betik hello aşağıdaki eylemleri gerçekleştirir:

* Merhaba depolama hesabı hello core-site.xml yapılandırmasında hello küme zaten varsa, hello betik çıkar ve başka hiçbir eylem gerçekleştirilir.

* Merhaba depolama hesabı var ve başlangıç anahtarı kullanılarak erişilebilir doğrular.

* Başlangıç anahtarı Hello küme kimlik bilgilerini kullanarak şifreler.

* Merhaba depolama hesabı toohello core-site.xml dosyasının ekler.

* Durdurur ve hello Oozie, YARN, MapReduce2 ve HDFS hizmetleri yeniden başlatır. Durdurma ve bu hizmetleri başlatma toouse hello yeni depolama hesabı sağlar.

> [!WARNING]
> Merhaba Hdınsight kümesi farklı bir konumda bir depolama hesabıyla desteklenmiyor.

## <a name="hello-script"></a>Merhaba komut dosyası

__Komut dosyası konumu__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)

__Gereksinimleri__:

* Merhaba üzerinde Hello betik uygulanan __baş düğümler__.

## <a name="toouse-hello-script"></a>toouse hello komut dosyası

Bu komut dosyası veya Azure CLI 1.0 hello hello Azure portal, Azure PowerShell kullanılabilir. Daha fazla bilgi için bkz: Merhaba [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) belge.

> [!IMPORTANT]
> Merhaba özelleştirme belgede sağlanan hello adımları kullanırken, bilgi tooapply aşağıdaki hello bu komut dosyasını kullanın:
>
> * Bu komut dosyası (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh) için URI hello herhangi örnek betik eylemi URI değiştirin.
> * Örnek parametreleri hello Azure depolama hesabı adı ve hello depolama hesabı toobe eklenen toohello kümesinin anahtarı ile değiştirin. Azure portal kullanarak Merhaba, bu parametreler boşlukla ayrılmış olması gerekir.
> * Bu komut dosyası olarak toomark gerekmez __kalıcı__, doğrudan hello Ambari yapılandırma hello kümesi için güncelleştirmeler.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a>Azure portalından veya Araçlar görüntülenmeyen depolama hesapları

Görüntüleme hello Hdınsight küme hello Azure portal, hello seçme __depolama hesapları__ altında girdisi __özellikleri__ bu betik eylemi eklenen depolama hesaplarına görüntülemez. Azure PowerShell ve Azure CLI hello ek depolama alanı hesabı ya da görüntülenmez.

Merhaba betik hello core-site.xml yapılandırma hello kümesi için yalnızca değiştirdiğinden hello depolama bilgiler görüntülenmiyor. Bu bilgiler, Azure yönetim API'leri kullanılarak hello küme bilgilerini alırken kullanılmaz.

Bu komut, kullanım hello Ambari REST API kullanarak toohello küme tooview depolama hesabı bilgilerini eklendi. Aşağıdaki komutları tooretrieve hello kümeniz için bu bilgileri kullanın:

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> Ayarlama `$clusterName` hello Hdınsight kümesi toohello adı. Ayarlama `$storageAccountName` hello depolama hesabının toohello adı. İstendiğinde, hello küme oturum açma (Yönetici) ve parola girin.

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> Ayarlama `$PASSWORD` toohello küme oturum açma (Yönetici) hesap parolası. Ayarlama `$CLUSTERNAME` hello Hdınsight kümesi toohello adı. Ayarlama `$STORAGEACCOUNTNAME` hello depolama hesabının toohello adı.
>
> Bu örnekte [curl (http://curl.haxx.se/)](http://curl.haxx.se/) ve [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve ve parse JSON verileri.

Bu komut, kullanırken değiştirin __CLUSTERNAME__ hello Hdınsight kümesi hello adı. Değiştir __parola__ hello küme oturum açma parolasını hello HTTP ile. Değiştir __STORAGEACCOUNT__ hello adıyla hello depolama hesabı betik eylemi kullanarak eklendi. Bu komuttan döndürülen bilgi metnini izleyen benzer toohello görünür:

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

Bu metin kullanılan şifreli bir anahtar örneğidir tooaccess hello depolama hesabı.

### <a name="unable-tooaccess-storage-after-changing-key"></a>Anahtar değiştirdikten sonra oluşturulamıyor tooaccess depolama

Bir depolama hesabının hello anahtarı değiştirirseniz, Hdınsight hello depolama hesabı artık erişemez. Hdınsight anahtarı önbelleğe alınmış bir kopyasını hello core-site.xml hello küme için kullanır. Önbelleğe alınan bu kopya güncelleştirilmiş toomatch hello yeni anahtarı olması gerekir.

Merhaba betik eylemi yeniden çalıştıran mu __değil__ hello depolama hesabı için bir giriş zaten varsa hello betik toosee denetler gibi hello anahtar güncelleştirin. Bir giriş zaten varsa, herhangi bir değişiklik yapmaz.

Bu soruna geçici bir çözüm toowork, varolan bir girişi hello hello depolama hesabı için kaldırmanız gerekir. Aşağıdaki adımları tooremove hello varolan bir girişi hello kullan:

1. Bir web tarayıcısında Hdınsight kümenizin hello Ambari Web kullanıcı arabirimini açın. Merhaba URI https://CLUSTERNAME.azurehdinsight.net ' dir. Değiştir __CLUSTERNAME__ kümenizin hello ada sahip.

    İstendiğinde, kümeniz için hello HTTP oturum açma kullanıcısı ve parolayı girin.

2. Merhaba hello sayfasının hello soldaki hizmetlerin listesinden __HDFS__. Merhaba seçip __yapılandırmalar__ hello sayfasının hello Center'da sekmesi.

3. Merhaba, __filtre...__  değeri alanına, __fs.azure.account__. Bu toohello kümeye eklenmiş herhangi bir ek depolama alanı hesabı girişlerini döndürür. İki tür giriş vardır; __keyprovider__ ve __anahtar__. Her ikisi de hello depolama hesabı hello anahtar adının bir parçası olarak hello adını içerir.

    Merhaba adlı bir depolama hesabı örnek girdileri verilmiştir __mystorage__:

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. Merhaba kırmızı tooremove ihtiyacınız hello depolama hesabı için hello anahtarları tanımladıktan sonra kullanmak '-' hello girişi toodelete sağında simgesi toohello. Hello kullan __kaydetmek__ toosave değişikliklerinizi düğmesine tıklayın.

5. Değişiklikler kaydedildikten sonra hello betik eylemi tooadd hello depolama hesabı ve yeni anahtar değeri toohello küme kullanın.

### <a name="poor-performance"></a>Düşük performans

Merhaba depolama hesabı hello Hdınsight kümesi farklı bir bölgede ise, düşük performans karşılaşabilirsiniz. Bir farklı bir bölgeye gönderir ve ağ trafiğini hello bölgesel Azure veri merkezi dışında çapraz erişilirken verilerde gecikme getirebilir genel internet hello.

> [!WARNING]
> Merhaba Hdınsight kümesi farklı bir bölgede bir depolama hesabı kullanılması desteklenmez.

### <a name="additional-charges"></a>Ek ücretlere

Merhaba depolama hesabı Hdınsight kümesi hello daha farklı bir bölgede ise, Azure faturalama hakkında ek çıkış ücretlerini fark edebilirsiniz. Verileri bir bölgesel veri merkezi ayrıldığında bir çıkış ücret uygulanır. Merhaba trafik farklı bir bölgede başka bir Azure veri merkezi için hedeflenen olsa bile bu ücretsiz olarak uygulanır.

> [!WARNING]
> Merhaba Hdınsight kümesi farklı bir bölgede bir depolama hesabı kullanılması desteklenmez.

## <a name="next-steps"></a>Sonraki adımlar

Nasıl tooan olan bir Hdınsight kümesine tooadd ek depolama hesapları öğrendiniz. Betik eylemleri hakkında daha fazla bilgi için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md)
