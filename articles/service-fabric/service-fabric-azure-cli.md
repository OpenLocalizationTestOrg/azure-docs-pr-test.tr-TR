---
title: "Azure Service Fabric XPlat CLI ile çalışmaya başlama"
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
ms.openlocfilehash: ddf881f6c202a82a3f64773639aa29b660057f8d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-xplat-cli-to-interact-with-a-service-fabric-cluster"></a>Service Fabric kümeyle etkileşim kurmak için XPlat CLI kullanma

Service Fabric kümesi Linux'ta XPlat CLI kullanarak Linux makinelerden etkileşim kurabilirsiniz.

İlk adımı get git rep CLI en son sürümünü ve aşağıdaki komutları kullanarak yolunuzda ayarlayın:

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

Her komut destekliyorsa, bu komut için Yardım almak için komut adını yazabilirsiniz.
Otomatik Tamamlama komutlar için desteklenir. Örneğin, aşağıdaki komut, Yardım için tüm uygulama komutları sağlar. 

```sh
 azure servicefabric application 
```

Aşağıdaki örnekte gösterildiği gibi belirli bir komut için Yardım daha fazla filtreleyebilirsiniz:

```sh
 azure servicefabric application  create
```

CLI otomatik tamamlama etkinleştirmek için aşağıdaki komutları çalıştırın:

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

Aşağıdaki komutlar kümeye bağlanın ve kümedeki düğümlerin göster:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

Adlandırılmış parametreleri kullanmanız ve bunların ne olduğunu bulmak için bir komutundan sonra yazabilirsiniz--yardımcı olur. Örneğin:

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

Çoklu makine bir küme için bir makineden bağlanırken **değil parçası olan küme**, aşağıdaki komutu kullanın:

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

PublicIPorFQDN etiketi gerçek IP veya FQDN ile uygun şekilde değiştirin. Çoklu makine bir küme için bir makineden bağlanırken **olan kümesinin parçası**, aşağıdaki komutu kullanın:

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

Azure portalı üzerinden, Linux Service Fabric kümesi ile etkileşim kurmak için CLI oluşturulan veya PowerShell kullanabilirsiniz.

> [!WARNING]
> Bu kümeleri güvenli değil, bu nedenle, bir-kutusunu küme bildiriminde genel IP adresi ekleyerek açmakta.

## <a name="using-the-xplat-cli-to-connect-to-a-service-fabric-cluster"></a>Bir Service Fabric kümeye bağlanmak için XPlat CLI kullanma

Aşağıdaki Azure CLI komutları güvenli bir kümeye bağlanmak nasıl açıklar. Sertifika ayrıntılarını küme düğümlerinde bir sertifika ile eşleşmesi gerekir.

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

Sertifikanızı sertifika yetkilileri (CA) varsa, aşağıdaki örnekteki gibi--ca sertifikası path parametresi eklemeniz gerekir: 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

Birden fazla CA varsa, ayırıcı olarak virgül kullanın.

Sertifikadaki ortak adınızı bağlantı uç noktasının eşleşmiyorsa parametresi kullanabileceğinizi `--strict-ssl-false` aşağıdaki komutta gösterildiği gibi doğrulama atlamak için:

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

CA doğrulama atlamak istediğiniz varsa, ekleyebilirsiniz aşağıdaki komutta gösterildiği gibi Reddet yetkisiz yanlış parametre: 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

Bağlandıktan sonra kümeyle etkileşim kurmak için diğer CLI komutları çalıştırmak görebilmeniz gerekir.

## <a name="deploying-your-service-fabric-application"></a>Service Fabric uygulamanızı dağıtma

Kopyalama, kaydetme ve service fabric uygulaması başlatmak için aşağıdaki komutları yürütün:

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>Uygulamanızı yükseltme

İşlem benzer [Windows işlem](service-fabric-application-upgrade-tutorial-powershell.md)).

Yapı, kopyalama, kaydetme ve proje kök dizininde uygulamanızı oluşturun. Uygulama örneği olarak adlandırılmışsa `fabric:/MySFApp`ve MySFApp türdür, komutları aşağıdaki gibi olur:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

Uygulamanızda değişikliği yapın ve değiştirilen hizmeti yeniden derleyin.  Değiştirilen hizmetin bildirim dosyası (ServiceManifest.xml) hizmeti (ve kod veya yapılandırma ve verileri uygun şekilde) için güncelleştirilmiş sürümleri ile güncelleştirin. Ayrıca uygulama bildirimi (ApplicationManifest.xml) uygulama ve değiştirilen hizmet için güncelleştirilmiş sürüm numarasıyla değiştirin.  Şimdi, kopyalamak ve aşağıdaki komutları kullanarak güncelleştirilmiş uygulamanızı kaydetme:

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

Şimdi, aşağıdaki komutla uygulama yükseltme başlatabilirsiniz:

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

Şimdi SFX kullanarak uygulama yükseltmesi izleyebilirsiniz. Birkaç dakika içinde uygulamanız güncelleştirilmiş olur. Ayrıca, bir hata ile güncelleştirilmiş bir uygulamayı deneyin ve hizmet yapıda otomatik geri alma işlevselliği denetleyin.

## <a name="converting-from-pfx-to-pem-and-vice-versa"></a>PEM ve tersi yönde PFX dönüştürme

Farklı bir ortamda olabilir güvenli küme erişmek için yerel makinenizdeki (Windows veya Linux ile) bir sertifika yüklemeniz gerekebilir. Örneğin, bir Windows makineden ve güvenli bir Linux kümesi erişirken sertifikanızı PEM ve tersi yönde PFX dönüştürmeniz gerekebilir. 

PEM dosyasından bir PFX dosyasına dönüştürmek için aşağıdaki komutu kullanın:

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

Bir PFX dosyasını PEM dosyasına dönüştürmek için aşağıdaki komutu kullanın:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Ayrıntılar için [OpenSSL belgelerine](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) bakın.

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>Sorun giderme


### <a name="copying-of-the-application-package-does-not-succeed"></a>Uygulama paketi kopyalama başarılı değil

Olup olmadığını denetleyin `openssh` yüklenir. Varsayılan olarak, Ubuntu Masaüstü yüklü sahip değil. Aşağıdaki komutu kullanarak yükleyin:

```sh
sudo apt-get install openssh-server openssh-client**
```

Sorun devam ederse, PAM için ssh değiştirerek devre dışı bırakmayı deneyin `sshd_config` aşağıdaki komutları kullanarak dosya:

```sh
sudo vi /etc/ssh/sshd_config
#Change the line with UsePAM to the following: UsePAM no
sudo service sshd reload
```

Sorun devam ederse sayısını ssh oturumları aşağıdaki komutları yürüterek artırmayı deneyin:

```sh
sudo vi /etc/ssh/sshd\_config
# Add the following to lines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

(Platform ssh paketleri kopyalamak için kullandığından) ssh kimlik doğrulaması (parola) aksine henüz desteklenmeyen için anahtarları kullanarak parola kimlik doğrulaması yerine kullanın.

## <a name="next-steps"></a>Sonraki adımlar

[Geliştirme ortamını ayarlama ve Linux kümesi için Service Fabric uygulaması dağıtın.](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>İlgili makaleler

* [Service Fabric ve Azure CLI 2.0 ile çalışmaya başlama](service-fabric-azure-cli-2-0.md)
