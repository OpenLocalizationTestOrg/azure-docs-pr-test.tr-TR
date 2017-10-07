---
title: "bir uygulama hizmeti ortamı v1 web uygulamasında aaaCreate"
description: "Toocreate nasıl web uygulamaları ve bir uygulama hizmeti ortamı v1 uygulama hizmeti planlarında öğrenin"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 983ba055-e9e4-495a-9342-fd3708dcc9ac
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 322ef344517c54247b102fb4920e35645986ef98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a>Bir uygulama hizmeti ortamı v1 bir web uygulaması oluşturma

> [!NOTE]
> Uygulama hizmeti ortamı v1 hello hakkında makaledir.  Merhaba, daha kolay toouse ve daha güçlü altyapısı üzerinde çalışan uygulama hizmeti ortamı'nın daha yeni bir sürümü var. Merhaba yeni sürümü hakkında daha fazla ile Merhaba Başlat toolearn [giriş toohello uygulama hizmeti ortamı](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl toocreate web uygulamaları gösterir ve App Service planlarına bir [uygulama hizmeti ortamı v1](app-service-app-service-environment-intro.md) (ana). 

> [!NOTE]
> Toolearn nasıl istiyorsanız toocreate bir web uygulaması toodo gerekmez, ancak bir uygulama hizmeti ortamında görmek [bir .NET web uygulaması oluşturma](app-service-web-get-started-dotnet.md) veya hello birini ilgili öğreticiler diğer dilleri ve çerçeveleri için.
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici, bir uygulama hizmeti ortamı oluşturduğunuz varsayar. Henüz yapmadıysanız bkz [bir uygulama hizmeti ortamı oluşturma](app-service-web-how-to-create-an-app-service-environment.md). 

## <a name="create-a-web-app"></a>Web uygulaması oluşturma
1. Merhaba, [Azure Portal](https://portal.azure.com/), tıklatın **yeni > Web + mobil > Web uygulaması**. 
   
    ![][1]
2. Aboneliğinizi seçin.  
   
    Birden çok aboneliğiniz varsa unutmayın, toocreate uygulama hizmeti ortamınızı uygulamada bir gereksinim toouse hello hello ortamı oluşturulurken kullanılan aynı abonelik. 
3. Kaynak grubunu seçin veya oluşturun.
   
    *Kaynak grupları* , toomanage kurulurken faydalıdır ve bir birim olarak Azure kaynaklarını ilgili etkinleştir *rol tabanlı erişim denetimi* (RBAC) kuralları, uygulamalarınız için. Daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış][ResourceGroups]. 
4. Bir uygulama hizmeti planı oluşturun veya seçin.
   
    *Uygulama hizmeti planları* web uygulamaları yönetilen kümeleridir.  Fiyatlandırma seçtiğinizde, normalde ücret hello App Service planı toohello tek tek uygulamalar yerine uygulanan toohello fiyatıdır. Merhaba işlem için ödeme ana örnekleri toohello ana ayrılan ASP ile listelenen yerine.  Uygulama hizmeti planınızın hello örneklerinde ölçeklendirme tooscale hello bir web uygulaması örneklerinin sayısını ayarlama ve bu planında tüm hello web uygulamaları etkiler.  Site yuvaları veya VNET tümleştirme gibi bazı özellikler de hello planı içinde miktar kısıtlamaları vardır.  Daha fazla bilgi için bkz: [Azure App Service planlarına genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)
   
    Merhaba planı adı altında belirtilen hello konumu bakarak, App Service planlarına Merhaba, ana tanımlayabilirsiniz.  
   
    ![][5]
   
    Uygulama hizmeti ortamı'nda toouse zaten bir uygulama hizmeti planı istiyorsanız, o planı seçin. Bu öğreticinin bölümden hello toocreate yeni bir uygulama hizmeti planı istiyorsanız bkz [bir uygulama hizmeti ortamı'nda bir uygulama hizmeti planı oluştur](#createplan).
5. Web uygulamanız için Hello ad girin ve ardından **oluşturma**. 
   
    İse, ana ASE'de bir uygulamanın bir dış VIP hello URL'sini kullanır: [*sitename*]. [ *uygulama hizmeti ortamınızı adını*]. yerine p.azurewebsites.net [*sitename*]. azurewebsites.net
   
    Ana olması, ana uygulama hello bir iç VIP URL'yi kullanıyorsa: [*sitename*]. [ *ana oluşturma sırasında belirtilen alt etki alanı*]   
    Ana oluşturma sırasında ASP seçtikten sonra aşağıda güncelleştirme hello alt etki alanı görürsünüz **adı**

## <a name="createplan"></a>Bir uygulama hizmeti planı oluştur
Uygulama hizmeti ortamı'nda bir uygulama hizmeti planı oluşturduğunuzda, çalışan seçimlerinizi ASE'de paylaşılan çalışanlar olduğundan farklıdır.  toouse sahip hello hello toohello ana hello Yöneticisi tarafından ayrılan olanları çalışanlardır  Bu, yeni bir plan o toocreate anlamına gelir tüm planlarınızı zaten bu çalışan havuzunda daha fazla ayrılan çalışanların tooyour ana çalışan havuzu sayısından hello toplam örnekleri toohave gerekir.  Planınız, ana çalışan havuzu toocreate içinde yeterli çalışanları yoksa, bunları eklenen, ana yönetici tooget ile toowork gerekir.

Bir uygulama hizmeti ortamı tarafından barındırılan uygulama hizmeti planına sahip başka bir fark seçimi fiyatlandırma hello yetersizliğidir.  Bir uygulama hizmeti ortamı olduğunda hello sistem tarafından kullanılan işlem kaynakları için ödeme ve hello planlar için ek ücret, ortamda sahip değil.  Normalde, bir uygulama hizmeti planı oluşturduğunuzda, faturalama belirleyen bir fiyatlandırma planı seçin.  Bir uygulama hizmeti ortamı temelde içeriği oluşturabileceğiniz özel bir konum değil.  İçeriğinizi hello ortamı ve değil toohost için ücret ödersiniz.

Merhaba aşağıdaki yönergeleri toocreate bir uygulama hizmeti planınızı nasıl hello öğreticinin hello önceki bölümde açıklandığı gibi bir web uygulaması oluştururken gösterir.

1. Tıklatın **Yeni Oluştur** planı seçimi Arabirimi hello ve bir ana dışında normalde yaptığınız gibi planınız için bir ad sağlayın.
2. Merhaba ana konum seçiciden toouse istediğinizi seçin.
   
    Bir uygulama hizmeti ortamı temelde özel dağıtım konumu olduğundan, konum altında gösterilir. 
   
    ![][2]
   
    Başlangıç konumu Seçici ASE'de seçimi yaptıktan sonra uygulama hizmeti plan oluşturma UI hello güncelleştirir.  Merhaba konumu şimdi hello ana sistem hello adını ve hello bölge olarak ve planı Seçici fiyatlandırma hello bir çalışan havuzu Seçici ile değiştirilir gösterir.  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a>Bir çalışan havuzu seçme
Normalde Azure App Service'te ve bir uygulama hizmeti ortamı dışında bir adanmış fiyat planı hello seçimi kullanılabilir 3 işlem boyutları vardır.  Benzer biçimde, bir ana için çalışanı too3 havuzları tanımlayabilir ve bu çalışan havuzu için kullanılan hello işlem boyutu belirtin.  Ne anlamına ana olan uygulama hizmeti planınız için işlem boyutuyla fiyatlandırma planı seçmek yerine ne adlı seçtiğiniz hello kiracılar için bir *çalışan havuzunda*.  

Merhaba çalışan havuzu seçimi UI hello adının altında bu çalışan havuzu için kullanılan hello işlem boyutunu gösterir.  Merhaba kullanılabilir miktar başvuruyor toohow birçok işlem örnek, havuzda kullanmak için kullanılabilir.  Merhaba toplam havuzu olabilir gerçekte bu sayıdan fazla örneğe, ancak bu değer toosimply başvuruyor kaç kullanımda değildir.  Uygulama hizmeti ortamı tooadd tooadjust ihtiyacınız varsa daha fazla işlem kaynaklara bakın [uygulama hizmeti ortamınızı yapılandırma](app-service-web-configure-an-app-service-environment.md).

![][4]

Bu örnekte, yalnızca iki çalışan havuzlarında kullanılabilir görürsünüz. Merhaba ana yönetici bu iki alt havuzları halinde yalnızca ana ayrılan olmasıdır.  içine ayrılan VM'ler olduğunda hello üçüncü görüntülenebilir.  

## <a name="after-web-app-creation"></a>Sonra Web uygulaması oluşturma
Web uygulamaları çalıştıran ve hesaba toobe gereken bir ana uygulama hizmeti planları yönetmek için bazı noktalar vardır.  

Daha önce belirtildiği gibi hello hello ana hello sistem hello boyutu için sorumlu sahibi ve yeterli kapasitesi toohost hello olduğundan emin olmanın istenen uygulama hizmeti planları için sonuç olarak bunlar da sorumludur. Kullanılabilir hiçbir çalışanları varsa, yapmamayı mümkün toocreate uygulama hizmeti planınızın olması.  Ayrıca, web uygulamanızın yukarı doğru tooscaling budur.  Daha fazla örnekleri ihtiyacınız sonra uygulama hizmeti ortamı yönetici tooadd tooget olurdu daha fazla çalışanlar.

Web uygulaması ve uygulama hizmeti planı oluşturduktan sonra bir fikir tooscale olan bunun.  ASE'de her zaman, uygulamalarınız için uygulama hizmeti planı tooprovide hata toleransı toohave en az 2 örneklerini gerekir.  Bir uygulama hizmeti ölçeklendirme, bir ana planında aynı hello uygulama hizmeti planı kullanıcı Arabirimi üzerinden normal olarak hello olur.  Ölçeklendirme hakkında daha fazla bilgi için [nasıl tooscale bir web uygulamasını bir uygulama hizmeti ortamı](app-service-web-scale-a-web-app-in-an-app-service-environment.md)

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspnewwebapp.png
[2]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createasplocation.png
[3]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspselected.png
[4]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspworkerpool.png
[5]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/selectaspinase.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment
[ResourceGroups]: ../azure-resource-manager/resource-group-overview.md
[AzurePowershell]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
