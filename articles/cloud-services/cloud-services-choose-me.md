---
title: "aaaAzure seçenekleri - bulut Hizmetleri işlem | Microsoft Docs"
description: "Azure işlem barındırma seçenekleri ve nasıl çalıştıklarını hakkında bilgi edinin: App Service, Cloud Services ve sanal makineler"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
ms.assetid: ed7ad348-6018-41bb-a27d-523accd90305
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: e7f109a54c61cc2f37644d39a61d2d932a374587
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-choose-cloud-services-or-something-else"></a>Bulut Hizmetleri veya başka bir şey seçmem gerekir?
Azure Cloud Services hello seçim için mi? Azure uygulamalarını çalıştırmak için farklı barındırma modelleri sağlar. Her biri farklı bir hizmetler kümesini sağlar, böylece hangisini seçtiğinize bağlıdır tam olarak ne, çalıştığınız toodo.

[!INCLUDE [compute-table](../../includes/compute-options-table.md)]

<a name="tellmecs"></a>

## <a name="tell-me-about-cloud-services"></a>Bulut hizmetleri hakkında bilgi ver
Bulut Hizmetleri örneğidir [hizmet olarak Platform](https://azure.microsoft.com/overview/what-is-paas/) (PaaS). Gibi [uygulama hizmeti](../app-service-web/app-service-web-overview.md), ölçeklenebilir, güvenilir tasarlanmış toosupport uygulamaları ve ucuz toooperate bu teknolojisidir. Yalnızca bir uygulama hizmeti Vm'lerinde, bu nedenle barındırılan gibi çok bulut Hizmetleri olan ancak hello VM'ler daha fazla denetime sahip olursunuz. Bulut hizmeti Vm'lerinde kendi yazılım yükleyebilir ve uzak içine kullanabilirsiniz.

![cs_diagram](./media/cloud-services-choose-me/diagram.png)

Daha fazla denetim ayrıca daha az kullanım kolaylığı anlamına gelir. Merhaba ek denetim seçeneklerini gerekmedikçe genellikle daha hızlı ve kolay tooget bir web uygulaması olduğundan ve App Service'te Web uygulamalarını çalışan tooCloud Hizmetleri karşılaştırılır.

Bulut hizmeti rolleriyle iki tür vardır. Merhaba yalnızca arasındaki hello iki rolünüze hello sanal makineye nasıl barındırılan farktır.

* **Web rolü**  
Otomatik olarak dağıtır ve uygulamanızı IIS üzerinden barındırır.

* **Çalışan rolü**  
IIS kullanmaz ve uygulama bağımsız çalıştırır.

Örneğin, bir basit uygulama yalnızca bir tek bir web rolü, bir Web sitesi hizmet veren kullanabilir. Daha karmaşık bir uygulama bir web rolü toohandle kullanabilir, kullanıcılardan gelen istekleri ardından geçirmek bu istekleri işlemek için tooa çalışan rolü. (Bu iletişim kullanmayı [Service Bus](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md) veya [Azure kuyrukları](../storage/common/storage-introduction.md).)

Hello önceki şekil önerir, tüm VM'ler hello aynı bulut hizmeti hello çalıştıran tek bir uygulama içinde. Tek bir ortak IP adresi, istekte bulunan aracılığıyla kullanıcılara erişim hello uygulama otomatik olarak yük dengeli hello uygulamanın VM'ler arasında. Merhaba platform [ölçeklendirir ve dağıtır](cloud-services-how-to-scale.md) tek bir donanım hatası noktası önler şekilde bulut Hizmetleri uygulamasında VM'ler hello.

Uygulamaları sanal makinelerinde çalışan karşın, bulut Hizmetleri PaaS, değil Iaas sağlar önemli toounderstand geçerlidir. Tek yönlü toothink ilgili şöyledir: Iaas, gibi Azure sanal makineleri ile ilk oluşturmak ve uygulamanızın çalıştığı hello ortamı yapılandırın, ardından uygulamanız bu ortamına dağıtma. Her VM hello işletim sistemi düzeltme eki yeni sürümlerini dağıtma gibi işlemler, bu world çoğunu yönetmekten sorumlu. PaaS içinde aksine, bu hello ortamın zaten gibi olur. Tüm toodo sahip olduğu uygulamanızı dağıtmak. Yönetim, hello işletim sistemi, yeni sürümlerini dağıtma dahil olmak üzere çalıştırdığı hello platformun sizin için işlenir.

## <a name="scaling-and-management"></a>Ölçeklendirme ve yönetim
Bulut Hizmetleri ile sanal makineleri oluşturmayın. Bunun yerine, her kaç, gibi istediğiniz Azure söyleyen bir yapılandırma dosyası girin **üç rol örnekleri web** ve **iki çalışan rolü örnekleri**, ve hello platform bunu sizin için yaratır.  Hala seçtiğiniz [boyutu](cloud-services-sizes-specs.md) bu sanal makineleri yedekleme olmalı, ancak siz açıkça bunları kendiniz oluşturmayın. Uygulamanızı toohandle yükü gerekirse, daha fazla VM'ler için isteyebilir ve bu örnekleri Azure oluşturur. Merhaba yükü azaltır, bu örneklerde kapatın ve bunlar için ödeme durdurun.

Bulut Hizmetleri uygulaması genellikle iki adımlı bir işlem aracılığıyla kullanılabilir toousers yapılır. Bir geliştirici ilk [karşıya hello uygulama](cloud-services-how-to-create-deploy.md) toohello platform alanı hazırlama. Hello Geliştirici hazır olduğunda toomake Merhaba uygulaması dinamik olarak ile üretim hello Azure portal tooswap hazırlama kullanırlar. Bu [hazırlama ve üretim arasında geçiş yapma](cloud-services-nodejs-stage-application.md) yükseltilmiş tooa yeni sürümü kullanıcılarına adresine olmadan çalışan bir uygulama sağlar kapalı kalma süresi olmadan yapılabilir.

## <a name="monitoring"></a>İzleme
Bulut hizmetleri de sağlar izleme. Azure sanal makineleri gibi başarısız bir fiziksel sunucuda algılar ve sunucuda yeni bir makine üzerinde çalışmakta olan hello VM'ler yeniden başlatır. Ancak bulut Hizmetleri başarısız VM'ler ve uygulamalar, yalnızca donanım hataları algılar. İsteğe bağlı olarak sanal makineleri farklı olarak, her web ve çalışan rolü içindeki bir aracıya sahip, ve bu nedenle bu mümkün toostart yeni VM'ler ve hatalar oluştuğunda uygulama örnekleri.

Bulut Hizmetleri PaaS yapısını Hello çok diğer etkilere sahiptir. Merhaba en önemli web veya çalışan rolü örneklerine başarısız olduğunda bu teknoloji üzerinde oluşturulan uygulamaların toorun doğru yazılmalıdır olduğunu biridir. Bu, uygulama döndürmemelidir korumak bulut Hizmetleri durum tooachieve hello kendi VM'ler dosya sistemi. Azure sanal makineler ile oluşturulan sanal makineleri tooCloud Hizmetleri VM'ler yapılan yazma kalıcı değildir; hiçbir şey bir sanal makine veri diski gibi yoktur. Bunun yerine, uygulama açıkça gereken bir bulut Hizmetleri tüm durum tooSQL veritabanı yazma BLOB, tablo veya başka bir harici depolama. Bu şekilde uygulamaları derleme onları daha kolay tooscale ve daha dirençli toofailure bulut Hizmetleri, her iki önemli hedeflerini hale getirir.

## <a name="next-steps"></a>Sonraki adımlar
[.NET içinde bir bulut hizmeti uygulaması oluşturma](cloud-services-dotnet-get-started.md)  
[Node.js içinde bir bulut hizmeti uygulaması oluşturma](cloud-services-nodejs-develop-deploy-app.md)  
[PHP ile bir bulut hizmeti uygulaması oluşturma](../cloud-services-php-create-web-role.md)  
[Python içinde bir bulut hizmeti uygulaması oluşturma](cloud-services-python-ptvs.md)

