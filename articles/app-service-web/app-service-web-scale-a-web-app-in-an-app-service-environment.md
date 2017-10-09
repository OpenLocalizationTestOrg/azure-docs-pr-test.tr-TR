---
title: "aaaHow tooScale bir uygulamada bir uygulama hizmeti ortamı"
description: "Bir uygulama hizmeti ortamı'nda bir uygulama ölçeklendirme"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 08916eac056c46bf8cb6edffbf96285317b32062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a>App Service Ortamında uygulamaları ölçeklendirme
Hello Azure uygulama hizmeti normal şekilde ölçeklendirebilirsiniz üç şey vardır:

* plan fiyatlandırması
* çalışan boyutu 
* örnek sayısı.

ASE'de planı fiyatlandırma hiçbir gerek tooselect ya da değişiklik hello yoktur.  Özellikleri bakımından Premium yetenek düzeyi fiyatlandırma zaten var.  

Saygı tooworker boyutlarıyla hello ana Yöneticisi her çalışan havuzu için kullanılan hello işlem kaynak toobe hello boyutunu atayabilirsiniz.  P4 işlem kaynakları ile çalışan havuzu 1 olabilir ve çalışan Havuz 2 P1 ile işlem kaynakları, isterseniz anlamına gelir.  Harici boyutu sırayla toobe gerekmez.  İçin hello boyutları ve bunların fiyatlandırma ayrıntılarla hello belgeyi buraya bakın [Azure App Service fiyatlandırması][AppServicePricing].  Bu, bir uygulama hizmeti ortamı toobe web uygulamaları ve App Service planları için seçeneklerinde ölçeklendirme hello bırakır:

* çalışan havuzu seçimi
* örnek sayısı

Her iki öğeyi değiştirme hello yapılır uygun App Service planları, ana barındırılan için gösterilen UI.  

![][1]

ASP bulunduğu hello çalışan havuzunda kullanılabilir işlem kaynakları hello sayısı ötesinde, ASP ölçeklendirin olamaz.  İşlem kaynaklarını çalışan havuzda varsa, ana yönetici tooadd tooget gereksinim bunları.  Buraya hello bilgileri, ana yeniden yapılandırma geçici bilgileri okumak için: [nasıl tooConfigure uygulama hizmeti ortamı][HowtoConfigureASE].  Merhaba ana otomatik ölçeklendirme özelliklerini tooadd kapasite zamanlama veya ölçümleri temelinde tootake avantajı da isteyebilirsiniz.  otomatik ölçeklendirme hello ana ortamı kendisi için yapılandırma hakkında daha fazla ayrıntı görmek tooget [nasıl tooconfigure otomatik bir uygulama hizmeti ortamı için ölçeklendirme][ASEAutoscale].

Birden çok uygulama farklı çalışan havuzlarından işlem kaynakları kullanılarak hizmet planları oluşturabilir veya kullanabilirsiniz hello aynı çalışan havuzu.  Örnek çalışan (10) kullanılabilir hesaplama kaynaklarınız varsa Havuz 1, (6) işlem kaynakları kullanılarak toocreate bir uygulama hizmeti planı seçin ve ikinci bir uygulama hizmeti planı (4) işlem kaynaklarını kullanır.

### <a name="scaling-hello-number-of-instances"></a>Örnek ölçeklendirme hello sayısı
Uygulama hizmeti ortamı'nda ilk web uygulamanızı oluşturduğunuzda ile 1 bir örneğini başlatır.  Tooadditional örnekleri tooprovide ek genişleme işlem sonra uygulamanız için kaynakları kullanabilirsiniz.   

Ana yeterli kapasitesi varsa, daha sonra bu oldukça basittir.  Tooyour tooscale yedeklemek istediğiniz ve imleyin hello siteleri tutan App Service planı gidin.  Bu hello buradan el ile ASP hello ölçek kümesi veya ASP için otomatik ölçeklendirme kurallarını yapılandırma kullanıcı arabirimini açar.  Uygulamanızı yalnızca ayarlayın toomanually ölçek ***göre Ölçeklendirmeniz*** çok***el ile girdiğim bir örnek sayısı***.  Buradan hello kaydırıcı istenen toohello miktar sürükleyin veya hello kutusunu sonraki toohello kaydırıcı girin.  

![][2] 

Bunlar her zamanki gibi bir ana iş bir ASP hello otomatik ölçeklendirme kurallarını aynı hello.  Seçebileceğiniz ***CPU yüzdesi*** altında ***göre Ölçeklendirmeniz*** ve CPU yüzdesi veya, göre ASP kullanarak daha karmaşık kurallar oluşturabilirsiniz için otomatik ölçeklendirme kuralları oluşturmak ***zamanlama ve performans kuralları ***.  toosee fazla otomatik ölçeklendirme kullanım hello Kılavuzu burada yapılandırma hakkında ayrıntılar tamamlamak [bir uygulama Azure App Service'te ölçeklendirme][AppScale]. 

### <a name="worker-pool-selection"></a>Çalışan havuzu seçimi
Daha önce belirtildiği gibi hello çalışan havuzu seçimi hello ASP UI ' erişilir.  Merhaba tooscale istediğiniz ve çalışan havuzu seçin ASP Hello dikey penceresini açın.  Tüm uygulama hizmeti ortamı'nda yapılandırılan hello çalışan havuzlarında görürsünüz.  Yalnızca bir çalışan havuzu varsa listelenen hello bir havuz yalnızca görürsünüz.  toochange hangi çalışan havuzu ASP, bu, App Service planı toomove istediğiniz hello çalışan havuzunda seçmeniz yeterlidir.  

![][3]

Bir çalışan havuzu tooanother ASP taşımadan önce önemli toomake, ASP için yeterli kapasiteye sahip emin olur.  Çalışan havuzlarında listesi Merhaba, yalnızca listelenen hello çalışan havuzu adı ancak, kaç tane çalışanları, çalışan havuzunda kullanılabilir olduğunu görebilirsiniz.  Yeterli örnekleri kullanılabilir toocontain uygulama hizmeti planınız emin olun.  Daha fazla işlem kaynaklarını hello çalışan havuzunda varsa, ana yönetici tooadd almak için toomove istediğiniz bunları.  

> [!NOTE]
> ASP hello uygulamalarda, bir çalışan havuzundan bir ASP soğuk neden olacak taşıma başlatır.  Uygulamanızı hello yeni işlem kaynakları üzerinde çalışmaya soğuk olduğundan bu yavaş istekler toorun neden olabilir.  Merhaba cold start hello kullanılarak önlenebilir [uygulama yeteneğini sıcak] [ AppWarmup] Azure App Service'te.  Yeni işlem kaynakları üzerinde çalışmaya uygulamaları soğuk olduğunda hello başlatma işlemi de çağrılan çünkü hello makalesinde açıklanan hello uygulama başlatma modül soğuk başlıyor de çalışır. 
> 
> 

## <a name="getting-started"></a>Başlarken
Uygulama hizmeti ortamları ile çalışmaya tooget bakın [nasıl tooCreate bir uygulama hizmeti ortamı][HowtoCreateASE]

Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service][AzureAppService].

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
