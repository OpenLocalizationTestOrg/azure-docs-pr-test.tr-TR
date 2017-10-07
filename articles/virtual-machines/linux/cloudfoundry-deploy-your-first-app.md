---
title: aaaDeploy ilk uygulama tooCloud Foundry Microsoft Azure | Microsoft Docs
description: "Bir uygulama tooCloud Foundry Azure üzerinde dağıtma"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a>İlk app tooCloud Foundry Microsoft Azure üzerinde dağıtma

[Bulut Foundry](http://cloudfoundry.org) popüler açık kaynak uygulama platformu Microsoft Azure üzerinde kullanılabilir. Bu makalede, gösteriyoruz nasıl toodeploy ve uygulamayı bulut Foundry üzerinde bir Azure ortamı yönetin.

## <a name="create-a-cloud-foundry-environment"></a>Bir bulut Foundry ortam oluşturma

Azure üzerinde bir bulut Foundry ortamı oluşturmak için birkaç seçenek vardır:

- Kullanım hello [Bileşendirler bulut Foundry teklif] [ pcf-azuremarketplace] hello Azure Marketi toocreate PCF Ops Manager ve hello Azure hizmet aracısı içeren standart bir ortam içinde. Bulabileceğiniz [tamamlamak yönergeleri] [ pcf-azuremarketplace-pivotaldocs] hello Market dağıtmak için hello Bileşendirler belgelerine sunar.
- Tarafından özelleştirilmiş bir ortam oluşturmak [Bileşendirler bulut Foundry el ile dağıtma][pcf-custom].
- [Merhaba açık kaynak bulut Foundry paketlerini doğrudan dağıtma] [ oss-cf-bosh] ayarıyla bir [BOSH](http://bosh.io) director hello dağıtım hello bulut Foundry ortamının koordine eden bir VM.

> [!IMPORTANT] 
> Azure Market hello PCF dağıtıyorsanız, hello SYSTEMDOMAINURL not edin ve tooaccess Bileşendirler uygulamaları Yöneticisi, her ikisi de hello Market Dağıtım Kılavuzu'nda açıklanan hello hello yönetici kimlik bilgileri gerekir. Bunlar Bu öğreticide gerekli toocomplete şunlardır. Market dağıtımları için hello SYSTEMDOMAINURL hello form https://system ' dir. *IP adresi*. cf.pcfazure.com.

## <a name="connect-toohello-cloud-controller"></a>Toohello bulut denetleyicisi Bağlan

Merhaba bulut denetleyicisi uygulamaları dağıtma ve yönetme için hello birincil giriş noktası tooa bulut Foundry ortamıdır. Merhaba çekirdek bulut denetleyicisi API (CCAPI), REST API olmakla birlikte çeşitli araçları üzerinden erişilebilir. Bu durumda, biz ile Merhaba etkileşim [bulut Foundry CLI][cf-cli]. Linux, MacOS veya Windows hello CLI yükleyebilirsiniz, ancak hiç, bu durumda kullanılabilir hello önceden yüklenmiş tooinstall tercih ederseniz [Azure bulut Kabuk][cloudshell-docs].

' de, toolog başına `api` toohello hello Market dağıtımından elde SYSTEMDOMAINURL. Merhaba varsayılan dağıtım otomatik olarak imzalanan bir sertifika kullandığından, ayrıca hello içermelidir `skip-ssl-validation` geçin.

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

İstendiğinde toolog toohello bulut denetleyicisi içinde var. Merhaba Market dağıtım adımları aldığınız hello yönetici hesabı kimlik bilgileri kullanın.

Bulut Foundry sağlar *düzenlemeler* ve *alanları* ad alanları tooisolate hello ekipleri ve paylaşılan bir dağıtım ortamlarında olarak. Merhaba PCF Market dağıtım içerir hello varsayılan *sistem* org ve bir dizi alanları hello otomatik ölçeklendirmeyi hizmet ve hello Azure hizmet aracısı gibi hello temel bileşenler toocontain oluşturuldu. Şimdilik, hello seçin *sistem* alanı.


## <a name="create-an-org-and-space"></a>Bir kuruluş oluşturup alanı

Yazarsanız, `cf apps`, hello sistem Krlş. Sistem boşluğu hello olarak dağıtılan sistem uygulamaları bakın 

Merhaba tutmalısınız *sistem* org sistem uygulamalar için ayrılmış örnek uygulamamız dolayısıyla bir kurum ve alan toohouse oluşturun.

```bash
cf create-org myorg
cf create-space dev -o myorg
```

Merhaba hedef komutu tooswitch toohello yeni org ve alan kullanın:

```bash
cf target -o testorg -s dev
```

Şimdi, bir uygulamayı dağıttığınızda, otomatik olarak hello yeni org ve alanı oluşturulur. şu anda tooconfirm hiçbir alanındaki hello yeni org/türdeki `cf apps` yeniden.

> [!NOTE] 
> Merhaba düzenlemeler ve alanları ve rol tabanlı erişim denetimi (RBAC) bunlar nasıl kullanılabileceği hakkında daha fazla bilgi için bkz: [bulut Foundry belgelerine][cf-orgs-spaces-docs].

## <a name="deploy-an-application"></a>Uygulama dağıtma

Java'da yazılmış ve hello üzerinde temel Hello yay bulut adlı örnek bir bulut Foundry uygulama kullanalım [yay Framework](http://spring.io) ve [yay önyükleme](http://projects.spring.io/spring-boot/).

### <a name="clone-hello-hello-spring-cloud-repository"></a>Merhaba Hello yay bulut depoyu kopyalayın

Merhaba Hello yay bulut örnek uygulama, GitHub üzerinde kullanılabilir. Tooyour ortam kopyalamak ve hello yeni dizine değiştirin:

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a>Merhaba uygulaması oluşturma

Yapı hello uygulamasını kullanarak [Apache Maven](http://maven.apache.org).

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a>Merhaba uygulama cf itme oluşturup dağıtın

Çoğu uygulamalar tooCloud Foundry dağıtabilirsiniz hello kullanarak `push` komutu:

```bash
cf push
```

Olduğunda, *itme* bir uygulama, bulut Foundry (Bu durumda, bir uygulamasında Java) uygulamasının hello türü algılar ve bağımlılıklarını (Framework'teki bu durumda, hello yay) tanımlar. Bunu daha sonra her şeyi paketleri olarak bilinen bir tek başına kapsayıcı görüntüsü kodunuzu toorun gerekli bir *Damlacık*. Son olarak, bulut Foundry zamanlamaları hello kullanılabilir makineleri ortamınızdaki birindeki uygulama hello ve size, hello hello komut çıktısında kullanılabilir olduğu ulaşabilecekleri bir URL oluşturur.

![Cf itme komut çıktısı][cf-push-output]

toosee Merhaba hello yay bulut uygulaması, tarayıcınızda açık hello sağlanan URL:

![Merhaba yay bulut için varsayılan kullanıcı Arabirimi][hello-spring-cloud-basic]

> [!NOTE] 
> toolearn sırasında neler olduğu hakkında daha fazla `cf push`, bkz: [uygulamaları nasıl hazırlanır] [ cf-push-docs] hello bulut Foundry belge içinde.

## <a name="view-application-logs"></a>Uygulama günlüklerini görüntüle

Merhaba bulut Foundry CLI tooview günlükleri için bir uygulama adıyla kullanabilirsiniz:

```bash
cf logs hello-spring-cloud
```

Varsayılan olarak, komut kullanır hello günlüklerini *tail*, yazıldığı gibi yeni günlükler gösterir. toosee yeni günlükler görünen hello hello yay bulut uygulamayı hello tarayıcıda yenileyin.

yazılan tooview günlükleri eklemek hello `recent` geçin:

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a>Merhaba uygulamayı Ölçeklendir

Varsayılan olarak, `cf push` yalnızca uygulamanızın tek bir örneğini oluşturur. tooensure yüksek kullanılabilirlik ve yüksek verimlilik için etkinleştir ölçek genişletme, uygulamalarınızı bir örneğine birden çok toorun genellikle istersiniz. Zaten dağıtılmış uygulamalarının hello kullanarak kolayca ölçeklendirebilirsiniz `scale` komutu:

```bash
cf scale -i 2 hello-spring-cloud
```

Çalışan hello `cf app` Merhaba uygulaması komutunda gösterir bulut Foundry hello uygulama başka bir örneği oluşturmaktır. Merhaba uygulaması başladıktan sonra bulut Foundry Yük Dengeleme trafik tooit otomatik olarak başlar.


## <a name="next-steps"></a>Sonraki adımlar

- [Okuma hello bulut Foundry belgeleri][cloudfoundry-docs]
- [Hello Visual Studio Team Services eklentisi için bulut Foundry ayarlayın][vsts-plugin]
- [Merhaba Microsoft günlük analizi kafa bulut Foundry için yapılandırma][loganalytics-nozzle]

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png