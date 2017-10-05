---
title: "Azure App Service planlarına ayrıntılı genel bakış | Microsoft Docs"
description: "Azure uygulama hizmeti iş için nasıl uygulama hizmeti planları ve bunların, yönetim deneyimi nasıl yararlı öğrenin."
keywords: "app service, azure app service, ölçek, ölçeklenebilir, app service planı, app service maliyeti"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: f97be571d104e3cc1c6ee732886fa7133ba0dc83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a>Azure App Service planlarına ayrıntılı genel bakış

Uygulama hizmeti planları, uygulamalarınızı barındırmak için kullanılan fiziksel kaynakları koleksiyonunu temsil eder.

App Service planları şunları tanımlar:

- Bölge (Batı ABD, Doğu ABD, vb.)
- Ölçek sayısı (bir, iki, üç örnekleri, vb.)
- (Küçük, Orta, büyük) örnek boyutu
- SKU (Ücretsiz, Paylaşılan, Temel, Standart, Premium)

İçinde Apps, Mobile Apps, API uygulamaları, işlev uygulamalarının (veya işlevler), web [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) bir uygulama hizmeti planındaki tüm çalışma.  Aynı abonelikte ve bölgede uygulamalarda uygulama hizmeti planı paylaşabilir. 

Tüm uygulamalar için atanan bir **uygulama hizmeti planı** tanımladığı kaynakları paylaşır. Bu paylaşımı para birden fazla uygulama tek bir uygulama hizmeti planında barındırdığında kaydeder.

Bu sırada **App Service planınızı** **Ücretsiz** ve **Paylaşılan** SKU’larından **Temel**, **Standart** ve **Premium** SKU’larına ölçeklendirerek daha fazla kaynak ve özelliğe erişebilirsiniz.

Uygulama hizmeti planınızı ayarlanmışsa **temel** SKU veya daha yüksek kontrol edebilirsiniz sonra **boyutu** ve ölçeklendirme VM'ler sayısı.

Örneğin, planınız standart hizmet katmanında iki "küçük" örneklerini kullanmak için yapılandırdıysanız, bu planla ilişkili tüm uygulamalar hem örneklerinde çalıştırın. Uygulamalar ayrıca standart hizmet katmanı özelliklerine erişime sahiptir. Plan örneği uygulamaları çalıştırdığınız tam olarak yönetilen ve yüksek oranda kullanılabilir.

> [!IMPORTANT]
> App Service planının **SKU** ve **Ölçek** değeri, planda barındırılan uygulama sayısını değil planın maliyetini belirler.

Bu makalede katmanı ve bir uygulama hizmeti planı ve nasıl uygulamalarınızı yönetmeye çalışırken oyuna geldikleri ölçek gibi anahtar özelliklerini inceler.

## <a name="apps-and-app-service-plans"></a>Uygulamalar ve uygulama hizmeti planları

Uygulama hizmeti bir uygulamada verilen herhangi bir zamanda yalnızca bir uygulama hizmeti plan ile ilişkili olabilir.

Uygulamaları ve planları içerdiği bir **kaynak grubu**. Bir kaynak grubu içinde olan her kaynak için yaşam döngüsü sınırı olarak görev yapar. Bir uygulamanın tüm parçaları birlikte yönetmek için kaynak gruplarını kullanabilirsiniz.

Tek bir kaynak grubu birden çok uygulama hizmeti planları olduğundan farklı uygulamalar farklı fiziksel kaynaklara tahsis edebilirsiniz.

Örneğin, geliştirme, test ve üretim ortamları arasında kaynakları ayırabilirsiniz. Üretim ve geliştirme ve test için ayrı ortamlara sahip kaynakları ayırmanıza olanak tanır. Bu şekilde, uygulamalarınızı yeni bir sürümü karşı test yük gerçek müşteriler hizmet veren, üretim uygulamalarınızı aynı kaynaklara için rekabet edemez.

Tek bir kaynak grubu içinde birden çok planına sahip olduğunuzda, coğrafi bölgeler kapsayan bir uygulama da tanımlayabilirsiniz.

Örneğin, iki bölgelerde çalışan yüksek oranda kullanılabilir bir uygulama, en az iki planları, her bölge için bir tane ve her plan ile ilişkili bir uygulama içerir. Böyle bir durumda, uygulamanın tüm kopyalarını ardından tek bir kaynak grubu içinde yer alır. Birden çok planları ve birden çok uygulama ile bir kaynak grubu olması yönetmek, denetlemek ve uygulama durumunu görüntülemek kolaylaştırır.

## <a name="create-an-app-service-plan-or-use-existing-one"></a>Bir uygulama hizmeti planı oluşturun veya varolan bir kullanın

Bir uygulama oluşturduğunuzda, bir kaynak grubu oluşturmayı düşünebilirsiniz. Öte yandan, bu uygulama daha büyük bir uygulama için bir bileşen varsa, bu büyük uygulama için ayrılmış kaynak grubunda oluşturun.

Uygulama bir tamamen yeni uygulama ya da daha büyük bir parçası olup olmadığını da barındırmak veya yeni bir tane oluşturmak için var olan bir planı kullanmayı seçebilirsiniz. Daha fazla kapasite ve beklenen yükü soru karardır.

Yeni bir uygulama hizmeti uygulamanızı yalıtma öneririz ne zaman planlama:

- Yoğun bir kaynak uygulamasıdır.
- Uygulama, var olan bir planı barındırılan diğer uygulamalardan farklı ölçeklendirme Etkenler vardır.
- Uygulamanın farklı bir coğrafi bölgede kaynak gerekir.

Böylece uygulamanız için yeni bir kaynak kümesini ayırmak ve uygulamalarınızın daha fazla denetim kazanmak.

## <a name="create-an-app-service-plan"></a>App Service planı oluşturma

> [!TIP]
> Bir uygulama hizmeti ortamı varsa, App Service ortamları için belirli şuradaki belgelere gözden geçirebilirsiniz: [bir uygulama hizmeti ortamı'nda bir uygulama hizmeti planı oluştur](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)

Uygulama hizmeti planı gözatma deneyimi veya uygulaması oluşturma işleminin bir parçası olarak boş bir uygulama hizmeti planı oluşturabilirsiniz.

İçinde [Azure portal](https://portal.azure.com), tıklatın **yeni** > **Web + mobil**ve ardından **Web uygulaması** veya diğer uygulama hizmeti uygulaması türü.

![Azure Portalı'nda bir uygulama oluşturun.][createWebApp]

Ardından, seçin veya yeni uygulaması için uygulama hizmeti planı oluşturun.

 ![Bir uygulama hizmeti planı oluşturun.][createASP]

Bir uygulama hizmeti planı oluşturmak için tıklatın **[+] oluştur yeni**, türü **uygulama hizmeti planı** adlandırın ve ardından uygun bir seçin **konumu**. Tıklatın **fiyatlandırma katmanı**ve ardından hizmet için uygun bir fiyatlandırma katmanı seçin. Seçin **tüm görüntüle** daha seçenekleri gibi fiyatlandırma görünümüne **serbest** ve **paylaşılan**. Fiyatlandırma katmanı seçtikten sonra tıklatın **seçin** düğmesi.

## <a name="move-an-app-to-a-different-app-service-plan"></a>Bir uygulama için farklı bir uygulama hizmeti planı taşıma

Bir uygulama farklı bir uygulama hizmeti planında taşıyabilirsiniz [Azure portal](https://portal.azure.com). Aynı kaynak grubunu ve coğrafi bölge planları olduğu sürece, uygulamaları planları arasında taşıyabilirsiniz.

Bir uygulamayı başka bir plana taşımak için:

- Taşımak istediğiniz uygulamaya gidin.
- İçinde **menü**, Ara **App Service planı** bölümü.
- Seçin **değişiklik uygulama hizmeti planı** işlemini başlatmak için.

**Uygulama hizmeti planını Değiştir** açılır **uygulama hizmeti planı** Seçici. Bu noktada, bu uygulamaya taşımak için var olan bir planı seçebilirsiniz.

> [!IMPORTANT]
> Select uygulama hizmeti planı kullanıcı Arabirimi, aşağıdaki ölçütlere göre filtrelenen:
> - Aynı kaynak grubunda var
> - Aynı coğrafi bölgede var
> - İçinde aynı Web alanı var.
>
> Bir Web alanı, sunucu kaynaklarını gruplandırması tanımlayan bir App Service içinde mantıksal bir yapıdır. Coğrafi bölge (örneğin, Batı ABD), uygulama hizmeti kullanan müşteriler ayırmak için birçok Web alanları içeriyor. Şu anda, uygulama hizmeti kaynaklar arasında izlemiyor taşınmasını mümkün değil.
>

![Uygulama hizmeti planı Seçici.][change]

Her plan kendi fiyatlandırma katmanı vardır. Örneğin, bir site ücretsiz katmanından bir taşıma için standart katmanı, özellikleri ve kaynakları standart katmanı kullanmak için atanmış tüm uygulamaları etkinleştirir.

## <a name="clone-an-app-to-a-different-app-service-plan"></a>Bir uygulama için farklı bir uygulama hizmeti plan kopyalama

Farklı bir bölgeye uygulama taşımak istiyorsanız, bir uygulama alternatiftir kopyalama. Kopyalama, yeni veya var olan uygulama hizmeti planındaki tüm bölgelerdeki uygulamanızı bir kopyasını oluşturur.

Bulabileceğiniz **kopya uygulama** içinde **geliştirme araçları** menüsünün bölümünde.

> [!IMPORTANT]
> Kopyalama sırasında hakkında bilgi edinebilirsiniz bazı sınırlamalara sahiptir [Azure portalını kullanarak Azure uygulama hizmeti kopyalama](../app-service-web/app-service-web-app-cloning-portal.md).

## <a name="scale-an-app-service-plan"></a>Ölçek bir uygulama hizmeti planı

Bir planı ölçeklendirmek için üç yolu vardır:

- **Fiyatlandırma katmanı değişikliği plan**. Bir planı temel katmandaki, standart ve standart katmanı özellikleri kullanmak için atanmış tüm uygulamalar için dönüştürülebilir.
- **Planın örnek boyutunu değiştirin**. Örnek olarak, büyük örnekleri kullanmak için bir plan küçük örnekleri kullanan temel katmandaki değiştirilebilir. Şimdi bu planla ilişkili tüm uygulamalar, büyük örnek boyutu sunar CPU kaynaklarını ve ek bellek kullanabilirsiniz.
- **Planın örnek sayısı değiştirme**. Örneğin, üç örneklerine giden ölçeklendirilmiş bir standart planı 10 örneklerine genişletilebilir. Premium planı 20 örneklerine (tabi kullanılabilirlik) genişletilebilir. Şimdi bu planla ilişkili tüm uygulamalar, büyük örnek sayısı sunar CPU kaynaklarını ve ek bellek kullanabilirsiniz.

Fiyatlandırma katmanı ve örnek boyutunu tıklatarak değiştirebilirsiniz **ölçeği Artır** uygulamayı veya uygulama hizmeti planı ayarları altında öğesi. Değişiklikler için uygulama hizmeti planı uygulamak ve onu barındıran tüm uygulamaları etkiler.

 ![Bir uygulama ölçeklendirmek için değerleri ayarlayın.][pricingtier]

## <a name="app-service-plan-cleanup"></a>Uygulama hizmeti planı temizleme

> [!IMPORTANT]
> **Uygulama hizmeti planları** sahip olan işlem kapasitesini yedek devam beri hala ücretlendirme kendileri için ilişkilendirilmiş uygulama yok.

Bir uygulama hizmeti planında barındırılan son uygulama silindiğinde beklenmeyen ücretlerden kaçınmak için sonuç boş uygulama hizmeti planı de silinir.

## <a name="summary"></a>Özet

Uygulama hizmeti planları, bir özellik kümesini ve Web siteleriniz arasında paylaşabileceğiniz kapasite temsil eder. Uygulama hizmeti planları bir kaynak grubu için belirli uygulamaları ayırmak ve daha fazla Azure kaynak kullanımınızı iyileştirmek için esneklik sağlar. Bu şekilde, test ortamınızda, tasarruf istiyorsanız bir planı birden çok uygulama arasında paylaşabilirsiniz. Ayrıca verimlilik, üretim ortamınız için birden çok bölgeler ve planları arasında ölçeklendirme tarafından en üst düzeye çıkarabilirsiniz.

## <a name="whats-changed"></a>Yapılan değişiklikler

- Sitelerinden App Service'e değiştirme kılavuzu için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
