---
title: "aaaUse hello Azure Machine Learning Web Hizmetleri portalı | Microsoft Docs"
description: "Erişim tooAzure Machine Learning çalışma alanlarını, yönetmek ve dağıtmak ve ML API web hizmetleri yönetme"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: jhubbard
editor: cgronlun
ms.assetid: b62cf2ca-dd2a-4a83-bb54-469f948fb026
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: v-donglo
ms.openlocfilehash: 04b49027fc0ab227382b320310088bb66aafacc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-service-using-hello-azure-machine-learning-web-services-portal"></a>Hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetme
Merhaba Microsoft Azure Machine Learning Web Hizmetleri portalı kullanarak, Machine Learning yeni ve Klasik Web Hizmetleri yönetebilir. Klasik Web Hizmetleri ve yeni Web hizmetleri üzerinde farklı temel alınan teknoloji dayandığından, biraz farklı yönetim özellikleri bunların her biri için var.

Merhaba Machine Learning Web Hizmetleri portalında şunları yapabilirsiniz:

* Merhaba web hizmeti nasıl kullanıldığını izleyin.
* Merhaba açıklama yapılandırın, hello web hello tuşları güncelleştirme hizmet (yalnızca yeni), günlük, depolama hesabı anahtar (yalnızca yeni), etkinleştirme güncelleştirmek ve etkinleştirmek veya devre dışı örnek verileri.
* Merhaba web hizmetini silin.
* Delete veya update faturalama (yalnızca yeni) planları oluşturun.
* Ekleme ve silme uç noktalar (yalnızca klasik)

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-toomanage-new-resources-manager-based-web-services"></a>İzinleri toomanage Yeni Kaynak Yöneticisi'ni web hizmetleri tabanlı

Yeni web Hizmetleri, Azure kaynakları olarak dağıtılır. Bu nedenle, hello doğru izinleri toodeploy sahip ve yeni web hizmetleri yönetin.  toodeploy, atanmalıdır katkıda bulunan yeni web hizmetleri yönetmek veya yönetici rolü hello abonelik toowhich hello web hizmeti üzerinde dağıtılır. Başka bir kullanıcı tooa machine learning çalışma alanı davet etmek, dağıtmak veya web hizmetleri yönetmek için önce bunları hello abonelik tooa katkıda bulunan veya yönetici rolü atamalısınız. 

Merhaba kullanıcı izinleri tooaccess kaynakları hello Azure Machine Learning Web Hizmetleri portalında düzeltmek hello sahip değilse, bunlar hello toodeploy bir web hizmeti çalışırken aşağıdaki hata alırsınız:

*Web hizmet dağıtımı başarısız oldu. Bu hesabın yeterli erişim toohello hello çalışma içeren Azure abonelik yok. Sırayla toohello çalışma toodeploy aynı hesap olmalıdır hello bir Web hizmeti tooAzure davet ve hello çalışma içeren verilen erişim toohello Azure aboneliğinizin olması.*

Bir çalışma alanı oluşturma hakkında daha fazla bilgi için bkz: [oluşturma ve Paylaşım bir Azure Machine Learning çalışma alanı](machine-learning-create-workspace.md).

Erişim izinlerini ayarlama hakkında daha fazla bilgi için bkz: [hello Azure portal - genel Önizleme alanındaki kullanıcılar ve gruplar için erişim atamalarını görüntüle](../active-directory/role-based-access-control-manage-assignments.md).


## <a name="manage-new-web-services"></a>Yeni Web Hizmetleri yönetme
toomanage, yeni Web Hizmetleri:

1. İçinde toohello oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) Microsoft Azure hesabınız - ile ilişkili hello hesabını kullan kullanarak portal hello Azure aboneliği.
2. Başlangıç menüsünde **Web Hizmetleri**.

Aboneliğiniz için dağıtılan Web Hizmetleri listesini görüntüler. 

toomanage bir Web hizmeti, Web Services'ı tıklatın. Merhaba Web Hizmetleri sayfasından şunları yapabilirsiniz:

* Merhaba web hizmeti toomanage'ı tıklatın.
* Merhaba faturalama planı hello web hizmeti tooupdate'ı tıklatın.
* Bir web hizmeti silin.
* Bir web hizmeti kopyalayın ve tooanother bölgesi dağıtın.

Bir web hizmeti tıklattığınızda hello web hizmeti hızlı başlangıç sayfasını açar. Hello web hizmeti hızlı başlangıç sayfası, web hizmetiniz toomanage izin iki menü seçenek vardır:

* **PANO** -tooview Web hizmeti kullanımına izin verir.
* **Yapılandırma** - hello depolama hesabı, Web hizmeti ile Merhaba ilişkili tooadd açıklayıcı metin, güncelleştirme hello anahtarını verir ve etkinleştirme veya devre dışı örnek verileri.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Merhaba web hizmeti nasıl kullanıldığını izleme
Merhaba tıklatın **PANO** sekmesi.

Merhaba panodan bir süre boyunca, Web hizmetinin genel kullanım görüntüleyebilirsiniz. Merhaba dönem açılır menüsünden hello sağ üst köşesinde, hello kullanım grafiklerini hello dönem tooview seçebilirsiniz. Başlangıç Panosu aşağıdaki bilgilerle hello gösterir:

* **Zaman içinde istekleri** süre seçili hello istekleri hello sayısının adım grafiği görüntüler. Bu, kullanımında ani karşılaşıyorsanız tanımlamaya yardımcı olabilir.
* **İstek-yanıt istekleri** hello toplam hello hizmet hello seçilen zaman aralığı ve bunlardan kaç tanesinin başarısız üzerinden aldı istek-yanıt çağrısı sayısını görüntüler.
* **Ortalama istek-yanıt işlem süresi** hello zaman ortalamasını görüntüleyen gerekli tooexecute alınan hello istekleri.
* **Toplu istekleri** hello toplam sayısını görüntüler toplu istekleri hello hizmet süre seçili hello aldı ve kaç tanesinin başarısız oldu.
* **Ortalama iş gecikme süresi** hello zaman ortalamasını görüntüleyen gerekli tooexecute alınan hello istekleri.
* **Hataları** çağrıları toohello web hizmetinde hello toplama oluşan hata sayısını gösterir.
* **Hizmetleri maliyetleri** hello hizmetiyle ilişkili hello fatura planı için hello ücretleri görüntüler.

### <a name="configuring-hello-web-service"></a>Merhaba web hizmetini yapılandırma
Merhaba tıklatın **yapılandırma** menü seçeneği.

Aşağıdaki özelliklere hello güncelleştirebilirsiniz:

* **Açıklama** tooenter hello Web hizmeti için bir açıklama sağlar.
* **Başlık** tooenter hello Web hizmeti için bir başlık sağlar
* **Anahtarları** toorotate sağlar, birincil ve ikincil API anahtarları.
* **Depolama hesabı anahtarı** hello Web hizmeti ile ilişkilendirilmiş hello depolama hesabının tooupdate hello anahtarı sağlar. 
* **Örnek verileri etkinleştirmek** tooprovide örnek verileri tootest hello istek-yanıt hizmeti kullanmanızı sağlar. Machine Learning Studio'da hello web hizmeti oluşturduysanız, hello örnek verileri kullanılan tootrain hello verilerden alınır, model. Merhaba hizmet program aracılığıyla oluşturduysanız, hello veri hello JSON paketinin bir parçası sağlanan hello örnek verileri alınır.

### <a name="managing-billing-plans"></a>Faturalandırma planları yönetme
Merhaba tıklatın **planları** hello web services hızlı başlangıç sayfasından menü seçeneği. Plan belirli Web hizmeti toomanage ile ilişkilendirilen hello planı de tıklayabilirsiniz.

* **Yeni** toocreate yeni bir plan sağlar.
* **Ekle/Kaldır Plan örneği** sağlar çok "var olan bir planı tooadd kapasite ölçeğini".
* **Yükseltme/indirgeme** sağlar çok "var olan bir planı tooadd kapasite ölçeği".
* **Silme** toodelete bir planı sağlar.

Bir planı tooview kendi Pano'ı tıklatın. Merhaba Pano belirli bir dönem anlık görüntü veya plan kullanım sağlar. tooselect zaman dönem tooview Merhaba, hello tıklatın **süresi** hello üst sağ tarafındaki panosu açılır. 

Merhaba plan Panosu aşağıdaki bilgilerle hello sağlar:

* **Plan açıklaması** hello maliyetleri ve kapasite hello planla ilişkili hakkındaki bilgileri görüntüler.
* **Plan kullanım** işlemleri ve hello plan ücret işlem saatleri hello sayısını görüntüler.
* **Web Hizmetleri** bu planı kullanarak Web Hizmetleri hello sayısını görüntüler.
* **İlk olarak Web hizmeti çağrıları** hello plan ücretlendirilen çağrıları yapma hello üst dört Web hizmetleri görüntüler.
* **Web Hizmetleri tarafından işlem sa üst** hello plan ücretlendirilen işlem kaynakları kullanılarak hello üst dört Web hizmetleri görüntüler.

## <a name="manage-classic-web-services"></a>Klasik Web Hizmetleri yönetme
> [!NOTE]
> Bu bölümdeki Hello yordamlar ilgili toomanaging Klasik web hizmetleri hello Azure Machine Learning Web Hizmetleri portalı üzerinden içindir. Klasik Web yönetme hakkında bilgi için Hizmetler aracılığıyla Machine Learning Studio hello'ı ve klasik Azure portalı, bkz: Merhaba [bir Azure Machine Learning çalışma alanını yönetme](machine-learning-manage-workspace.md).
> 
> 

toomanage, Klasik Web Hizmetleri:

1. İçinde toohello oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) Microsoft Azure hesabınız - ile ilişkili hello hesabını kullan kullanarak portal hello Azure aboneliği.
2. Başlangıç menüsünde **Klasik Web Hizmetleri**.

Klasik Web hizmeti toomanage tıklatın **Klasik Web Hizmetleri**. Merhaba Klasik Web Hizmetleri sayfasından şunları yapabilirsiniz:

* Merhaba web hizmeti tooview ilişkili hello uç'a tıklayın.
* Bir web hizmeti silin.

Klasik Web hizmeti yönetirken, her hello uç noktaları ayrı olarak yönetin. Bir web hizmeti hello Web Hizmetleri sayfasında tıklattığınızda hello hizmetiyle ilişkili uç noktaları hello listesi açılır. 

Merhaba Klasik Web Hizmeti uç noktası sayfasında, eklemek ve hello Hizmeti uç noktalarını silin. Uç noktaları ekleme hakkında daha fazla bilgi için bkz: [uç noktaları oluşturma](machine-learning-create-endpoint.md).

Merhaba uç noktaları tooopen hello web hizmeti hızlı başlangıç sayfasını birini tıklatın. Merhaba hızlı başlangıç sayfasında, web hizmetiniz toomanage izin iki menü seçeneği vardır:

* **PANO** -tooview Web hizmeti kullanımına izin verir.
* **Yapılandırma** -tooadd açıklayıcı metin, verir hello depolama hesabı, Web hizmeti ile Merhaba ilişkili hata oturum açma ve kapatma, güncelleştirme hello anahtarını açın ve etkinleştirme ve örnek verileri devre dışı.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Merhaba web hizmeti nasıl kullanıldığını izleme
Merhaba tıklatın **PANO** sekmesi.

Merhaba panodan bir süre boyunca, Web hizmetinin genel kullanım görüntüleyebilirsiniz. Merhaba dönem açılır menüsünden hello sağ üst köşesinde, hello kullanım grafiklerini hello dönem tooview seçebilirsiniz. Başlangıç Panosu aşağıdaki bilgilerle hello gösterir:

* **Zaman içinde istekleri** süre seçili hello istekleri hello sayısının adım grafiği görüntüler. Bu, kullanımında ani karşılaşıyorsanız tanımlamaya yardımcı olabilir.
* **İstek-yanıt istekleri** hello toplam hello hizmet hello seçilen zaman aralığı ve bunlardan kaç tanesinin başarısız üzerinden aldı istek-yanıt çağrısı sayısını görüntüler.
* **Ortalama istek-yanıt işlem süresi** hello zaman ortalamasını görüntüleyen gerekli tooexecute alınan hello istekleri.
* **Toplu istekleri** hello toplam sayısını görüntüler toplu istekleri hello hizmet süre seçili hello aldı ve kaç tanesinin başarısız oldu.
* **Ortalama iş gecikme süresi** hello zaman ortalamasını görüntüleyen gerekli tooexecute alınan hello istekleri.
* **Hataları** çağrıları toohello web hizmetinde hello toplama oluşan hata sayısını gösterir.
* **Hizmetleri maliyetleri** hello hizmetiyle ilişkili hello fatura planı için hello ücretleri görüntüler.

### <a name="configuring-hello-web-service"></a>Merhaba web hizmetini yapılandırma
Merhaba tıklatın **yapılandırma** menü seçeneği.

Aşağıdaki özelliklere hello güncelleştirebilirsiniz:

* **Açıklama** tooenter hello Web hizmeti için bir açıklama sağlar. Açıklama gerekli bir alandır.
* **Günlük kaydı** hello noktadaki günlüğü tooenable veya devre dışı bırakma hata verir. Günlüğe kaydetme hakkında daha fazla bilgi için bkz [Machine Learning web hizmetleri için günlüğe kaydetme](machine-learning-web-services-logging.md).
* **Örnek verileri etkinleştirmek** tooprovide örnek verileri tootest hello istek-yanıt hizmeti kullanmanızı sağlar. Machine Learning Studio'da hello web hizmeti oluşturduysanız, hello örnek verileri kullanılan tootrain hello verilerden alınır, model. Merhaba hizmet program aracılığıyla oluşturduysanız, hello veri hello JSON paketinin bir parçası sağlanan hello örnek verileri alınır.

## <a name="grant-or-suspend-access-tooweb-services-for-users-in-hello-portal"></a>Vermek veya erişimi tooWeb Hizmetleri kullanıcıları hello Portalı'nda askıya alma
Merhaba Klasik Azure portalı kullanarak izin verebilir veya toospecific kullanıcıların erişimini engellemek.

### <a name="access-for-users-of-new-web-services"></a>Kullanıcılar yeni Web Hizmetleri için erişim
tooenable diğer kullanıcıların toowork hello Azure Machine Learning Web Hizmetleri portal, Web Hizmetleri ile bunları ortak yöneticileri Azure aboneliğinize eklemeniz gerekir.

İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Microsoft Azure kullanarak hesap - hello Azure aboneliği ile ilişkili hello hesabı kullanın.

1. Merhaba Gezinti bölmesinde **ayarları**, ardından **Yöneticiler**.
2. Merhaba penceresinin Hello altında tıklatın **Ekle**. 
3. Hello bir ortak yönetici ekleme iletişim kutusu, ortak yönetici ve ortak yönetici tooaccess hello istediğiniz seçip hello abonelik tooadd istediğiniz hello kişinin hello e-posta adresini yazın.
4. **Kaydet** düğmesine tıklayın.

### <a name="access-for-users-of-classic-web-services"></a>Klasik Web Hizmetleri kullanıcıları için erişim
bir çalışma alanı toomanage:

İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Microsoft Azure kullanarak hesap - hello Azure aboneliği ile ilişkili hello hesabı kullanın.

1. Merhaba Microsoft Azure Hizmetleri panelinde tıklatın **MACHINE LEARNING**.
2. Merhaba çalışma toomanage istediğiniz'ı tıklatın.
3. Merhaba tıklatın **yapılandırma** sekmesi.

Merhaba yapılandırma sekmesinden, erişim toohello Machine Learning çalışma alanı tıklayarak askıya alabilirsiniz **REDDETME**. Kullanıcılar artık mümkün tooopen hello çalışma Machine Learning Studio'da olacaktır. toorestore erişim'i tıklatın **izin**.

toospecific kullanıcıları:

Machine Learning Studio'da erişim toohello çalışma sahip toomanage ek hesapları'nı tıklatın **oturum açma Studio tooML** hello içinde **PANO** sekmesi. Machine Learning Studio'da hello çalışma alanı açılır. Buradan hello tıklatın **ayarları** sekmesini ve ardından **kullanıcılar**. Tıklayabilirsiniz **daha fazla kullanıcı davet** toogive kullanıcılar toohello çalışma alanında, erişim veya bir kullanıcı seçin ve tıklatın **kaldırmak**.

> [!NOTE]
> Merhaba **oturum açma Studio tooML** bağlantısı, Machine Learning Studio hello Microsoft, şu anda oturumunuz içine Account kullanarak açar. Merhaba Microsoft toohello Azure Klasik portalı toocreate bir çalışma alanı toosign kullanılan Account bu çalışma izni tooopen otomatik olarak yok. bir çalışma alanı tooopen toohello hello çalışma hello sahibi olarak tanımlandı Microsoft Account içinde imzalanmalıdır veya tooreceive hello sahibi toojoin hello çalışma alanından bir davet gerekir.
> 
> 

