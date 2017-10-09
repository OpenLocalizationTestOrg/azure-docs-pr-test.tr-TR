---
title: "Azure Service Fabric XPlat CLI ile aaaGetting başlatıldı"
description: "Azure Service Fabric XPlat CLI ile çalışmaya başlama"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a>Service Fabric kümesi ile Merhaba XPlat CLI toointeract kullanma

Service Fabric kümesi Linux'ta hello XPlat CLI kullanarak Linux makinelerden etkileşim kurabilirsiniz.

Hello ilk adım olan Al hello CLI hello en son sürümünü hello git rep ve bunun yolu kullanarak hello komutları aşağıdaki kümesi:

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

Her komut destekliyorsa, bu komut için hello komut tooobtain hello Yardımı hello adı yazabilirsiniz.
Otomatik Tamamlama hello komutları için desteklenmiyor. Örneğin, tüm hello uygulama komutlar için Yardım komut verir aşağıdaki hello. 

```sh
 azure servicefabric application 
```

Aşağıdaki örnekte gösterildiği hello hello Yardım tooa belirli komut, daha fazla filtreleyebilirsiniz:

```sh
 azure servicefabric application  create
```

tooenable otomatik-tamamlama hello CLI, hello aşağıdaki komutları çalıştırın:

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

Aşağıdaki komutları hello toohello küme ve hello kümedeki düğümler hello Göster Bağlan:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

toouse adlandırılmış parametreleri ve bunların ne olduğunu bulun, yazabilirsiniz--Yardım komutundan sonra. Örneğin:

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

Tooa çoklu makine küme bir makineden bağlanırken **değil parçası olan hello küme**, komutu aşağıdaki hello kullanın:

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

Merhaba PublicIPorFQDN etiketi hello gerçek IP veya FQDN ile uygun şekilde değiştirin. Tooa çoklu makine küme bir makineden bağlanırken **hello kümesinin parçası olan**, komutu aşağıdaki hello kullanın:

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

Hello Azure portal CLI toointeract Linux Service Fabric kümesi ile oluşturulan veya PowerShell kullanabilirsiniz.

> [!WARNING]
> Bu kümeleri güvenli değil, bu nedenle, bir-kutusunu hello küme bildiriminde hello genel IP adresi ekleyerek açmakta.

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a>Merhaba XPlat CLI tooconnect tooa Service Fabric kümesi kullanma

Azure CLI komutları aşağıdaki hello nasıl tooconnect tooa güvenli küme açıklanmaktadır. Merhaba sertifika ayrıntıları hello küme düğümlerinde bir sertifika ile eşleşmesi gerekir.

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

Sertifikanızı sertifika yetkilileri (CA) varsa, aşağıdaki örneğine hello gibi tooadd hello--ca sertifikası path parametresi gerekir: 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

Birden fazla CA varsa, hello ayırıcı olarak virgül kullanın.

Merhaba sertifikadaki ortak adınızı hello bağlantı uç noktasının eşleşmiyorsa hello parametre kullanabilirsiniz `--strict-ssl-false` toobypass hello komutu aşağıdaki gösterildiği gibi doğrulama hello:

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

Tooskip hello CA doğrulama isterseniz hello--hello komutu aşağıdaki gösterildiği gibi Reddet yetkisiz yanlış parametre ekleyebilirsiniz: 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

Bağlandıktan sonra diğer CLI komutları toointeract ile mümkün toorun olmalıdır hello küme.

## <a name="deploying-your-service-fabric-application"></a>Service Fabric uygulamanızı dağıtma

Toocopy, kaydetme ve hello service fabric uygulaması Başlat komutlarını aşağıdaki hello yürütün:

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>Uygulamanızı yükseltme

Merhaba işlemdir benzer toohello [Windows işlem](service-fabric-application-upgrade-tutorial-powershell.md)).

Yapı, kopyalama, kaydetme ve proje kök dizininde uygulamanızı oluşturun. Uygulama örneği olarak adlandırılmışsa `fabric:/MySFApp`ve hello türdür MySFApp, hello komutları şu şekilde olacaktır:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

Tooyour uygulama değiştirmek ve değişiklik hello hizmeti yeniden hello olun.  Güncelleştirme hello hizmetin bildirim dosyası (ServiceManifest.xml) güncelleştirilmiş hello sürümleriyle hello hizmeti için (ve kod veya yapılandırma ve verileri uygun olarak) değiştirdi. Ayrıca hello güncelleştirilmiş sürüm numarasıyla Merhaba uygulaması için hello uygulama bildirimi (ApplicationManifest.xml) değiştirin ve değiştirilen hizmet hello.  Şimdi, kopyalayabilir ve güncelleştirilmiş uygulamanızı hello aşağıdaki komutları kullanarak kaydedin:

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

Şimdi, komutu aşağıdaki hello ile Merhaba uygulama yükseltme başlatabilirsiniz:

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

Şimdi hello uygulama yükseltme SFX kullanarak izleyebilirsiniz. Birkaç dakika içinde Merhaba uygulaması güncelleştirilmiş. Ayrıca, bir hata ile güncelleştirilmiş bir uygulamayı deneyin ve service fabric hello otomatik geri alma işlevselliği denetleyin.

## <a name="converting-from-pfx-toopem-and-vice-versa"></a>PFX tooPEM ve tersi yönde dönüştürme

Farklı bir ortamda olabilir, yerel makine (Windows veya Linux) tooaccess güvenli kümelerinde tooinstall sertifika gerekebilir. Örneğin, bir Windows makineden ve güvenli bir Linux kümesi erişirken tooconvert sertifikanızı PFX tooPEM ve bunun tersi de gerekebilir. 

PEM dosyası tooa PFX dosyası, komut aşağıdaki kullanım hello gelen tooconvert:

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

tooconvert dosyasından bir PFX dosyası tooa PEM, komutu aşağıdaki kullanım hello:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Çok başvuran[OpenSSL belgelerine](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) Ayrıntılar için.

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>Sorun giderme


### <a name="copying-of-hello-application-package-does-not-succeed"></a>Merhaba uygulama paketi kopyalama başarılı değil

Olup olmadığını denetleyin `openssh` yüklenir. Varsayılan olarak, Ubuntu Masaüstü yüklü sahip değil. Komutu aşağıdaki hello kullanarak yükleyin:

```sh
sudo apt-get install openssh-server openssh-client**
```

Merhaba sorun devam ederse, PAM için ssh hello değiştirerek devre dışı bırakmayı deneyin `sshd_config` hello aşağıdaki komutları kullanarak dosyası:

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

Merhaba sorun devam ederse, artan hello sayıda ssh oturumları hello aşağıdaki komutları yürüterek deneyin:

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

Tuşları kullanarak (Merhaba platform ssh toocopy paketleri kullandığından) ssh kimlik doğrulaması (olarak karşılıklı toopasswords) henüz desteklenmiyor, bu nedenle parola kimlik doğrulaması kullanın.

## <a name="next-steps"></a>Sonraki adımlar

[Merhaba geliştirme ortamını ayarlama ve bir Service Fabric uygulaması tooa Linux kümesi dağıtabilirsiniz.](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>İlgili makaleler

* [Service Fabric ve Azure CLI 2.0 ile çalışmaya başlama](service-fabric-azure-cli-2-0.md)
