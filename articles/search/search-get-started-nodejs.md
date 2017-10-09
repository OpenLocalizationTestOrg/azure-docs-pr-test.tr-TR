---
title: "Node.js içinde Azure Search ile çalışmaya aaaGet | Microsoft Docs"
description: "Programlama diliniz olarak Node.js kullanarak, Azure'da barındırılan bir bulut arama hizmeti üzerinde arama uygulaması derleme konusunu inceleyin."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a>Node.js'de Azure Search kullanmaya başlama
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Nasıl toobuild özel bir Node.js arama arama deneyimi için Azure Search kullanan uygulamayı öğrenin. Bu öğretici hello kullanır [Azure Search Hizmeti REST API'si](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello nesneleri ve bu alıştırmada kullanılan işlemleri.

Kullandık [Node.js](https://Nodejs.org) ve NPM, [Sublime Text 3](http://www.sublimetext.com/3)ve Windows 8.1 toodevelop'de Windows PowerShell ve bu kodu sınayın.

toorun hello için kaydolabilirsiniz bir Azure Search hizmeti bu örnek olmalıdır [Azure portal](https://portal.azure.com). Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) adım adım yönergeler için.

## <a name="about-hello-data"></a>Merhaba veri hakkında
Bu örnek uygulama hello verileri kullanan [Birleşik Devletler Jeoloji Hizmetleri (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrelenmiş hello Rhode Island eyaleti tooreduce hello veri kümesi boyutu. Bu veri toobuild akışlar, Göller ve zirveler gibi jeolojik özelliklerin yanı sıra hastaneler ve okullar gibi önemli binaları döndüren bir arama uygulaması kullanacağız.

Bu uygulamada hello **Dataındexer** programı oluşturup yükleri hello dizini kullanarak bir [dizin oluşturucu](https://msdn.microsoft.com/library/azure/dn798918.aspx) hello alma yapısı, filtrelenmiş USGS veri kümesini ortak bir Azure SQL veritabanından. Kimlik bilgileri ve bağlantı bilgileri toohello çevrimiçi veri kaynağına hello program kodu içinde sağlanır. Ek yapılandırma gerekli değildir.

> [!NOTE]
> Bu veri kümesi toostay hello 10.000 belge limiti hello ücretsiz fiyatlandırma katmanı altında üzerinde bir filtre uygulanmış. Merhaba standart katmanı kullanırsanız bu limit uygulanmaz. Her fiyatlandırma katmanının kapasitesi hakkında ayrıntılı bilgi için bkz: [Search hizmet limitleri](search-limits-quotas-capacity.md).
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Merhaba hizmet adı ve Azure Search hizmetinizin api anahtarını bulma
Merhaba hizmeti oluşturduktan sonra dönüş toohello portal tooget hello URL'si veya `api-key`. Bağlantıları tooyour arama hizmeti gerektiren her iki hello URL'ye sahip ve bir `api-key` tooauthenticate hello çağrısı.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba atlama çubuğunda, **Search Hizmeti** tüm Azure arama hizmetleri aboneliğiniz için sağlanan toolist.
3. Toouse istediğiniz hello hizmeti seçin.
4. Merhaba hizmet panosunda hello yönetici anahtarlarına erişim için anahtar simgesine hello gibi önemli bilgiler için kutucuklar görürsünüz.
5. Merhaba hizmet URL'si, bir yönetici anahtarını ve sorgu anahtarını kopyalayın. Toohello config.js. dosyasına eklerken, tüm üç daha sonra gerekir.

## <a name="download-hello-sample-files"></a>Merhaba örnek dosyalarını indirme
Her iki yaklaşım toodownload hello örnek aşağıdaki hello birini kullanın.

1. Çok Git[Azuresearchnodejsındexerdemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).
2. Tıklatın **ZIP'i indir**hello .zip dosyasını kaydedin ve ardından içerdiği tüm hello dosyaları ayıklayın.

Sonraki tüm dosya değişiklikleri ve çalıştırma deyimleri bu klasördeki dosyalara uygulanır.

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a>Merhaba config.js güncelleştirin. Search hizmetinizin URL'si ve api anahtarı ile güncelleştirme
URL ve daha önce kopyaladığınız api anahtarını hello kullanarak yapılandırma dosyasında hello URL, yönetici anahtarını ve sorgu anahtarını belirtin.

Yönetici anahtarları, dizin oluşturma ve silme ile belge yükleme de dahil olmak üzere hizmet işlemleri üzerinde tam denetim hakkı verir. Buna karşılık sorgu anahtarları tooAzure arama bağlanan istemci uygulamaları tarafından genellikle kullanılan salt okunur işlemler içindir.

Bu örnekte, anahtar toohelp pekiştirmek hello sorgu anahtarını istemci uygulamalarında kullanma hello en iyi uygulama olarak hello sorgu içerir.

Aşağıdaki ekran görüntüsü gösterildiği hello **config.js** hello ile bir metin düzenleyicisinde açın nerede tooupdate hello hello dosyasıyla değerden görebilmeniz için güncelleştireceğinizi ilgili girişler arama hizmetiniz için geçerli.

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a>Ana bilgisayar hello örnek için çalışma zamanı ortamı
Merhaba örnek genel olarak npm kullanarak yükleyebileceğiniz bir HTTP sunucusu gerektirir.

Bir PowerShell penceresinde aşağıdaki komutları hello için kullanın.

1. Merhaba içeren toohello klasörüne gidin **package.json** dosya.
2. `npm install` yazın.
3. `npm install -g http-server` yazın.

## <a name="build-hello-index-and-run-hello-application"></a>Merhaba dizini oluşturun ve hello uygulamayı çalıştırın
1. `npm run indexDocuments` yazın.
2. `npm run build` yazın.
3. `npm run start_server` yazın.
4. Tarayıcınızı `http://localhost:8080/index.html` adresine yönlendirin

## <a name="search-on-usgs-data"></a>USGS verilerinde arama
Merhaba USGS veri kümesini ilgili toohello Rhode Island eyaleti kayıtları içerir. Tıklatırsanız **arama** bir boş arama kutusunda, hello ilk 50 girişi hello varsayılan olduğu alırsınız.

Bir arama terimi girerek hello arama motoru toogo üzerinde bir şey sağlar. Bölgesel bir ad girmeyi deneyin. "Roger Williams", Rhode Island hello ilk İdarecisi oluştu. Çok sayıda parka, binaya ve okula onun adı verildi.

![][9]

Ayrıca, bu terimlerden herhangi birini de deneyebilirsiniz:

* Pawtucket
* Pembroke
* kaz + şapka

## <a name="next-steps"></a>Sonraki adımlar
Bu Node.js ve hello USGS veri kümesini temel alan hello ilk Azure Search öğreticisidir. Zaman içinde biz özel çözümlerinizde toouse isteyebilirsiniz ek arama özellikleri Bu öğretici toodemonstrate genişletmeniz.

Zaten Azure Search ile ilgili belirli bir altyapınız varsa öneri araçlarını (yazarken tamamlanan veya otomatik tamamlanan sorgular ), filtreleri ve çok yönlü gezinmeyi denemek için, bu örneği dayanak olarak kullanabilirsiniz. Ayrıca, numaralar ekleyerek ve böylece kullanıcılar hello sonuçları belgeleri toplu işleme hello arama sonuçları sayfasını artırabilir.

Yeni tooAzure arama? Diğer öğreticiler toodevelop bir neler yapabileceğinizi anlamak çalışırken öneririz. Ziyaret bizim [belge sayfasının](https://azure.microsoft.com/documentation/services/search/) toofind daha fazla kaynak. Merhaba bağlantılar da görüntüleyebilirsiniz bizim [Video ve öğretici listemiz](search-video-demo-tutorial-list.md) tooaccess daha fazla bilgi.

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
