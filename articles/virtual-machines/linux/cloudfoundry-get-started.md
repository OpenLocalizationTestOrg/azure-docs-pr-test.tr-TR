---
title: "Microsoft azure'da bulut Foundry başlangıç aaaGetting | Microsoft Docs"
description: "Microsoft Azure üzerinde OSS veya Bileşendirler bulut Foundry çalıştırın"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a>Azure’da Cloud Foundry

Bulut Foundry bir açık kaynak platform olarak-hizmet (PaaS) oluşturmak, dağıtmak ve çeşitli dilleri ve çerçeveleri geliştirilen uygulamaları 12 faktör işletim ' dir. Bu belgede Azure ve size nasıl başlayabiliriz bulut Foundry çalıştırmak için sahip hello seçenekler açıklanmaktadır.

## <a name="cloud-foundry-offerings"></a>Bulut Foundry teklifleri

Bulut Foundry kullanılabilir toorun Azure ile ilgili iki tür vardır: açık kaynak bulut Foundry (OSS CF) ve Bileşendirler bulut Foundry (PCF). OSS CF olan bir tamamen [açık kaynak](https://github.com/cloudfoundry) bulut Foundry sürümü hello bulut Foundry Foundation tarafından yönetilir. Bir kurumsal dağıtım bulut Foundry Bileşendirler yazılım Inc., bileşendirler bulut Foundry Bazı hello iki teklifleri hello farklarını arayın.

### <a name="open-source-cloud-foundry"></a>Açık kaynak bulut Foundry

Azure üzerinde OSS bulut Foundry BOSH yönetmenin ilk dağıtma ve hello kullanarak bulut Foundry dağıtma dağıtabilirsiniz [Github'da sağlanan yönergeleri](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md). OSS CF kullanma hakkında daha fazla toolearn bkz hello [belgelerine](https://docs.cloudfoundry.org/) hello bulut Foundry Foundation tarafından sağlanan.

Microsoft, topluluk kanalları aşağıdaki hello aracılığıyla OSS CF için en yüksek çaba destek sağlar:

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a>bosh azure CPI kanalda [bulut Foundry kayma](https://slack.cloudfoundry.org/)
- [cf bosh posta listesi](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- Hello için GitHub sorunları [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) ve [hizmet Aracısı](https://github.com/Azure/meta-azure-service-broker/issues)

>[!NOTE]
> Bulut Foundry çalıştırdığı hello sanal makineler gibi Azure kaynaklarınızı desteği Hello düzeyini Azure destek sözleşmenizi temel alır. En yüksek çaba topluluk desteği yalnızca toohello bulut Foundry özgü bileşenleri için geçerlidir.

### <a name="pivotal-cloud-foundry"></a>Bileşendirler bulut Foundry

Bileşendirler bulut Foundry hello içeren bir dizi özel yönetim araçları ve kurumsal destek birlikte hello OSS dağıtım olarak aynı çekirdek platformu. Azure üzerinde PCF toorun Pivotal lisanstan edinmeniz gerekir. Merhaba PCF hello Azure Market tekliften 90 günlük deneme lisansı içerir.

Merhaba araçlarda [Bileşendirler Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), dağıtımını ve bir bulut Foundry temel yönetimini kolaylaştıran bir web uygulaması ve [Bileşendirler uygulamaları Yöneticisi](https://docs.pivotal.io/pivotalcf/console/), yönetmek için bir web uygulaması Kullanıcılar ve uygulamalar.

Ayrıca toohello destek kanallarını, yukarıdaki OSS CF için listelenen PCF lisans, toocontact Pivotal desteği hakkı verir. Microsoft ve Pivotal toocontact izin destek iş akışları konusunda yardım almak için her iki taraf da etkinleştirdiyseniz ve burada hello sorunu arasındadır bağlı olarak uygun şekilde yönlendirilmesini, soru sahiptir.

## <a name="azure-service-broker"></a>Azure hizmet Aracısı

Bulut Foundry teşvik eden hello ["on iki öğeli uygulama"](https://12factor.net/) temiz ayrılması durum bilgisiz uygulama işlemleri ve durum bilgisi olan hizmetler yedekleme yükseltir Metodoloji. [Hizmet aracıların](https://docs.cloudfoundry.org/services/api.html) tutarlı bir yol tooprovision sunar ve yedekleme hizmetleri tooapplications bağlayın. Merhaba [Azure hizmet Aracısı](https://github.com/Azure/meta-azure-service-broker) hello bazıları Azure depolama ve Azure SQL dahil olmak üzere bu kanal üzerinden anahtar Azure hizmetleri sağlar.

Bileşendirler bulut Foundry kullanıyorsanız, hello hizmet aracısı ayrıca olduğu [kullanılabilir bir kutucuk olarak](https://docs.pivotal.io/azure-sb/installing.html) hello Bileşendirler ağ alanından.

## <a name="related-resources"></a>İlgili kaynaklar

### <a name="visual-studio-team-services-plugin"></a>Visual Studio Team Services eklentisi

Bulut Foundry hello kullanımını sürekli tümleştirme (CI) ve kesintisiz teslim (CD) dahil olmak üzere uygun tooagile yazılım geliştirme ' dir. Projelerinizi Visual Studio Team Services (VSTS) toomanage kullanıyorsanız ve tooset bulut Foundry hedefleme CI/CD işlem hattı kurmak istediğiniz, hello kullanabilirsiniz [VSTS bulut Foundry yapı uzantısı](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension). Merhaba eklentisi basit tooconfigure kolaylaştırır ve dağıtımları tooCloud Foundry, Azure veya başka bir çalışan olup olmadığını otomatikleştirmek ortamı.

## <a name="next-steps"></a>Sonraki adımlar

- [Azure Market hello Bileşendirler bulut Foundry dağıtma](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [Bir uygulama tooCloud azure'da Foundry dağıtma](./cloudfoundry-deploy-your-first-app.md)
