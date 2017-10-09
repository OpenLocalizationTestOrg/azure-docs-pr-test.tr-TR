---
title: "Node.js modüllerini ile aaaWorking"
description: "Bilgi nasıl toowork Azure uygulama hizmeti veya Bulut hizmetlerini kullanırken Node.js modüllerini ile."
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c0e6cd3d-932d-433e-b72d-e513e23b4eb6
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 926358b7eb80a659dbc1015686b06a30d8c9b8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-nodejs-modules-with-azure-applications"></a>Azure uygulamalarıyla Node.js Modüllerini kullanma
Bu belge, Azure üzerinde barındırılan uygulamalarıyla Node.js modüllerini kullanma yönergeleri sağlar. Ayrıca, uygulamanızda modülün belirli bir sürümünün kullanıldığından nasıl emin olacağınız ve Azure'la yerel modülleri nasıl kullanacağınız da anlatılır.

Node.js modüllerini kullanma ile bilginiz varsa **package.json** ve **npm shrinkwrap.json** dosyaları, aşağıdaki bilgilerle hello bu makalede ele alınan kısa bir Özet sağlar:

* Azure uygulama hizmeti anlar **package.json** ve **npm shrinkwrap.json** dosyaları ve bu dosyalardaki girişleri temel modülleri yükleyebilirsiniz.

* Azure bulut Hizmetleri beklediğiniz hello geliştirme ortamını ve hello yüklü tüm modüllerin toobe **düğümü\_modülleri** hello dağıtım paketinin bir parçası olarak dahil edilen dizin toobe. Modülleri kullanarak yüklemek için olası tooenable desteği olan **package.json** veya **npm shrinkwrap.json** dosyalarını bulut Hizmetleri; ancak, bu yapılandırma hello varsayılan özelleştirmesini gerektirir Bulut hizmeti projeleri tarafından kullanılan komutlar. Bir örnek için nasıl tooconfigure bu ortam bkz [Azure başlangıç görevi toorun npm yükleme tooavoid düğümü modülleri dağıtma](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)

> [!NOTE]
> Bir VM Hello dağıtım deneyimi hello sanal makine tarafından barındırılan hello işletim sistemine bağlı olarak bu makalede, azure sanal makineleri açıklanmamaktadır.
> 
> 

## <a name="nodejs-modules"></a>Node.js modüllerini
Modüller, uygulamanız için belirli işlevler sağlayan yüklenebilir JavaScript paketlerdir. Modüller, hello kullanarak genellikle yüklenir **npm** komut satırı aracı, ancak bazı modüller (örneğin, hello http Modülü) hello çekirdek Node.js paketinin bir parçası sağlanır.

Modülleri yüklendiğinde hello depolandıkları **düğümü\_modülleri** hello kökündeki uygulama dizin yapısının dizin. Her modül hello içinde **düğümü\_modülleri** directory tutar kendi **düğümü\_modülleri** bağlıdır ve bu davranış yinelenir tüm modülleri içeren dizini Her bir modül tüm hello şekilde hello bağımlılık zinciri Aşağı'ı için. Bu ortam, ancak bu oldukça büyük dizin yapısında sonuçlanabilir, bağlı olduğu kendi sürüm gereksinimlerini hello modülleri için her modül yüklü toohave sağlar.

Dağıtma hello **düğümü\_modülleri** uygulamanızın parçası karşılaştırıldığında hello dağıtım hello boyutu arttıkça dizin toousing bir **package.json** veya  **npm shrinkwrap.json** dosya; üretimde kullanılan hello modülleri hello sürümleri olan Merhaba, aynı geliştirme kullanılan hello modüllerle ancak garanti etmez.

### <a name="native-modules"></a>Yerel modülleri
Çoğu Modüller yalnızca düz metin JavaScript dosyaları olsa da, bazı platforma özgü ikili görüntülerini modüllerdir. Bu modüller yükleme zamanında Python ve düğüm gyp kullanarak genellikle derlenir. Azure Cloud Services üzerinde hello kullanan bu yana **düğümü\_modülleri** Merhaba uygulaması, hello yüklü modülleri parçası olduğu sürece bir bulut hizmetinde çalışması gerekir gibi dahil herhangi bir yerel modül bir parçası olarak dağıtılan klasörü yüklü ve bir Windows geliştirme sisteminde derlenir.

Azure uygulama hizmeti, tüm yerel modülleri desteklemez ve belirli önkoşulları modüllerle derlerken başarısız olabilir. MongoDB gibi bazı popüler modülleri isteğe bağlı yerel bağımlılıkları vardır ve onlar olmadan uygundur olsa da, iki geçici çözüm bugün neredeyse tüm yerel modülleri ile kullanılabilir başarılı oluyor uygulamasına yol açıyordu:

* Çalıştırma **npm yükleme** bir Windows makinesinde yüklü tüm hello yerel modülün önkoşulları vardır. Sonra oluşturulan hello dağıtmak **düğümü\_modülleri** klasörü hello uygulama tooAzure uygulama hizmeti bir parçası olarak.

  * Derleme önce yerel Node.js yüklemenizi eşleşen mimariye sahip ve hello sürüm olası toohello Azure'da kullanılan olduğunca yakın olup olmadığını denetleyin (Merhaba geçerli değerleri kontrol edileceği özelliklerinden çalışma zamanında **process.arch**ve **process.version**).

* Azure uygulama hizmeti yapılandırılmış tooexecute özel bash olabilir veya kabuk betikleri, vermiş, dağıtımı sırasında hello fırsat tooexecute özel komutlar ve tam olarak hello yapılandırabilirsiniz yolu **npm yükleme** çalıştırılıyor. Bir video gösteren için nasıl tooconfigure bu ortam bkz [özel Web sitesi dağıtım betikleri Kudu ile].

### <a name="using-a-packagejson-file"></a>Bir package.json dosyası kullanma
Merhaba **package.json** dosyasıdır uygulamanızın gerektirdiği hello barındırma platformuna hello bağımlılıkları yükleyebilmek için bir yol toospecify hello en üst düzey bağımlılıkları tooinclude hello gerektiren yerine **düğümü \_paketleri** klasörü hello dağıtımının bir parçası olarak. Merhaba uygulama dağıtıldıktan sonra hello **npm yükleme** komuttur kullanılan tooparse hello **package.json** dosya ve listelenen tüm hello bağımlılıkları yükler.

Geliştirme sırasında hello kullanabilirsiniz **--Kaydet**, **--Kaydet geliştirme**, veya **--Kaydet isteğe bağlı** modülleri tooadd hello modülü tooyour içinbirgirişyüklerkenparametreleri**package.json** dosya otomatik olarak. Daha fazla bilgi için bkz: [npm yükleme](https://docs.npmjs.com/cli/install).

Merhaba ile olası bir sorunu **package.json** dosyadır, yalnızca üst düzey bağımlılıklar için hello sürümünü belirtir. Her modül yüklü olabilir veya bağımlı hello modülleri hello sürümü yazamazlar ve bu nedenle, farklı bir bağımlılığı hello geliştirme kullanılan daha şunun, mümkündür.

> [!NOTE]
> TooAzure App Service, dağıtırken, <b>package.json</b> dosyaya başvuruda bulunan yerel bir modül aşağıdaki Git kullanarak hello uygulama yayımlarken örneğine bir hata benzer toohello görebilirsiniz:
> 
> npm hata! module-name@0.6.0yükleyin: 'düğümü gyp Yapılandır yapı'
> 
> npm hata! ' cmd "/ c" "düğümü gyp yapılandırma derleme" ' 1 ile başarısız oldu
> 
> 

### <a name="using-a-npm-shrinkwrapjson-file"></a>Bir npm shrinkwrap.json dosyası kullanma
Merhaba **npm shrinkwrap.json** dosyasıdır bir girişim tooaddress hello modülü sürüm oluşturma sınırlamaları hello **package.json** dosya. Merhaba sırasında **package.json** dosyası yalnızca içerir sürümleri hello üst düzey modüller için hello **npm shrinkwrap.json** dosyası hello tam modül bağımlılık zinciri hello sürüm gereksinimlerini içerir.

Uygulamanızın üretime hazır olduğunda, kilitleme sürüm gereksinimlerini ve oluşturma bir **npm shrinkwrap.json** hello kullanarak dosya **npm shrinkwrap** komutu. Bu komut hello yüklü hello sürümlerini kullanır **düğümü\_modülleri** klasörünü ve bu sürümleri toohello kayıt **npm shrinkwrap.json** dosya. Merhaba uygulaması barındırma ortamına dağıtılan toohello sağlandıktan sonra hello **npm yükleme** komuttur kullanılan tooparse hello **npm shrinkwrap.json** dosya ve listelenen tüm hello bağımlılıkları yükler. Daha fazla bilgi için bkz: [npm shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap).

> [!NOTE]
> TooAzure App Service, dağıtırken, <b>npm shrinkwrap.json</b> dosyaya başvuruda bulunan yerel bir modül aşağıdaki Git kullanarak hello uygulama yayımlarken örneğine bir hata benzer toohello görebilirsiniz:
> 
> npm hata! module-name@0.6.0yükleyin: 'düğümü gyp Yapılandır yapı'
> 
> npm hata! ' cmd "/ c" "düğümü gyp yapılandırma derleme" ' 1 ile başarısız oldu
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Anladığınıza göre Azure ile toouse Node.js modüllerini nasıl bilgi nasıl çok[hello Node.js sürümünü belirtme], [derleme ve Node.js web uygulamasına dağıtma](app-service-web/app-service-web-get-started-nodejs.md), ve [nasıl toouse hello Azure komut satırı Mac ve Linux için arabirimi].

Daha fazla bilgi için bkz: Merhaba [Node.js Geliştirici Merkezi](/nodejs/azure/).

[hello Node.js sürümünü belirtme]: nodejs-specify-node-version-azure-apps.md
[nasıl toouse hello Azure komut satırı Mac ve Linux için arabirimi]:cli-install-nodejs.md
[özel Web sitesi dağıtım betikleri Kudu ile]: https://channel9.msdn.com/Shows/Azure-Friday/Custom-Web-Site-Deployment-Scripts-with-Kudu-with-David-Ebbo
