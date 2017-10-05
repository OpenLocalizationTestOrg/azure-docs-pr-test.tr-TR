---
title: "Azure Machine Learning Web Hizmetleri Portalı'nı | Microsoft Docs"
description: "Azure Machine Learning çalışma alanları, erişimini yönetmek ve dağıtmak ve ML API web hizmetleri yönetme"
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
ms.openlocfilehash: ad1314aa4b504bd2cb3285789073d4f1de1f545d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-web-service-using-the-azure-machine-learning-web-services-portal"></a>Azure Machine Learning Web Hizmetleri Portalı'nı kullanarak bir Web hizmetini yönetme
Machine Learning yeni ve Microsoft Azure Machine Learning Web Hizmetleri Portalı'nı kullanarak Klasik Web hizmetleri yönetebilirsiniz. Klasik Web Hizmetleri ve yeni Web hizmetleri üzerinde farklı temel alınan teknoloji dayandığından, biraz farklı yönetim özellikleri bunların her biri için var.

Machine Learning Web Hizmetleri Portalı'nda aşağıdakileri yapabilirsiniz:

* Web hizmeti nasıl kullanıldığını izleyin.
* Açıklama yapılandırın, anahtarları güncelleştirme (yalnızca yeni) için web hizmeti, günlük, depolama hesabı anahtar (yalnızca yeni), etkinleştirme güncelleştirmek ve etkinleştirmek veya devre dışı örnek verileri.
* Web hizmeti silin.
* Delete veya update faturalama (yalnızca yeni) planları oluşturun.
* Ekleme ve silme uç noktalar (yalnızca klasik)

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-to-manage-new-resources-manager-based-web-services"></a>Yeni Kaynak Yöneticisi'ni yönetmek için izinleri web hizmetleri tabanlı

Yeni web Hizmetleri, Azure kaynakları olarak dağıtılır. Bu nedenle, dağıtmak ve yeni web hizmetleri yönetmek için doğru izinlere sahip olmalıdır.  Dağıtma veya yeni web hizmetleri yönetmek için bir web hizmeti dağıtıldığı abonelik katkıda bulunan veya yönetici rolü atanmalıdır. Machine learning çalışma alanı için başka bir kullanıcı davet, dağıtmak veya web hizmetleri yönetmek için önce bir abonelik katkıda bulunan veya yönetici rolü atamanız gerekir. 

Kullanıcı Azure Machine Learning Web Hizmetleri portalında kaynaklara erişmek için doğru izinlere sahip değilse, bunlar bir web hizmetini dağıtma çalışılırken aşağıdaki hatayı alırsınız:

*Web hizmet dağıtımı başarısız oldu. Bu hesap, çalışma alanı içeriyor Azure aboneliği için yeterli erişimi yok. Bir Web hizmeti Azure'a dağıtmak için aynı hesabı için çalışma alanına davet gerekir ve çalışma alanını içeren Azure aboneliğinize erişim verilmesi.*

Bir çalışma alanı oluşturma hakkında daha fazla bilgi için bkz: [oluşturma ve Paylaşım bir Azure Machine Learning çalışma alanı](machine-learning-create-workspace.md).

Erişim izinlerini ayarlama hakkında daha fazla bilgi için bkz: [kullanıcılar ve gruplar Azure portalında - genel Önizleme için erişim atamalarını görüntüle](../active-directory/role-based-access-control-manage-assignments.md).


## <a name="manage-new-web-services"></a>Yeni Web Hizmetleri yönetme
Yeni Web hizmetleri yönetmek için:

1. Oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) Microsoft Azure kullanarak portal hesabı - Azure aboneliğiyle ilişkili hesabı kullanın.
2. Menüsünde **Web Hizmetleri**.

Aboneliğiniz için dağıtılan Web Hizmetleri listesini görüntüler. 

Bir Web hizmetini yönetmek için Web Services'ı tıklatın. Web Hizmetleri sayfasından şunları yapabilirsiniz:

* Web hizmeti yönetmek için tıklatın.
* Faturalama güncelleştirmek için planlama web hizmeti için tıklatın.
* Bir web hizmeti silin.
* Bir web hizmeti kopyalayın ve başka bir bölgeye dağıtın.

Bir web hizmeti tıkladığınızda, web hizmeti hızlı başlangıç sayfasını açar. Web hizmeti hızlı başlangıç sayfası, web hizmetiniz yönetmenizi iki menü seçenek vardır:

* **PANO** -Web hizmeti kullanım görüntülemenize izin verir.
* **Yapılandırma** - açıklayıcı metin eklemenize olanak sağlayan Web hizmeti ile ilişkilendirilmiş depolama hesabına ait anahtar güncelleştirme ve etkinleştirmek veya örnek verileri devre dışı.

### <a name="monitoring-how-the-web-service-is-being-used"></a>Web hizmeti nasıl kullanıldığını izleme
Tıklatın **PANO** sekmesi.

Panodan bir süre boyunca, Web hizmetinin genel kullanım görüntüleyebilirsiniz. Sağ üst köşesinde kullanım grafiklerini dönem açılır menüsünden görüntülemek için dönemi seçebilirsiniz. Pano aşağıdaki bilgileri gösterir:

* **Zaman içinde istekleri** seçilen süre boyunca bir adım grafiği isteklerinin sayısını görüntüler. Bu, kullanımında ani karşılaşıyorsanız tanımlamaya yardımcı olabilir.
* **İstek-yanıt istekleri** hizmet seçilen zaman aralığı ve bunlardan kaç tanesinin başarısız üzerinden aldı istek-yanıt çağrıları toplam sayısını gösterir.
* **Ortalama istek-yanıt işlem süresi** alınan isteklerin yürütülebilmesi için gereken süre ortalama görüntüler.
* **Toplu istekleri** Batch hizmeti, seçilen zaman aralığı ve bunlardan kaç tanesinin başarısız üzerinden aldı istek toplam sayısını gösterir.
* **Ortalama iş gecikme süresi** alınan isteklerin yürütülebilmesi için gereken süre ortalama görüntüler.
* **Hataları** web hizmeti çağrıları ortaya çıkan hataları toplam sayısını görüntüler.
* **Hizmetleri maliyetleri** fatura planı hizmetiyle ilişkili ücretleri görüntüler.

### <a name="configuring-the-web-service"></a>Web hizmetini yapılandırma
Tıklatın **yapılandırma** menü seçeneği.

Aşağıdaki özellikler güncelleştirebilirsiniz:

* **Açıklama** Web hizmeti için bir açıklama girmenize olanak sağlar.
* **Başlık** Web hizmeti için bir başlık girmenize olanak sağlar
* **Anahtarları** birincil ve ikincil API anahtarlarınızı döndürmenizi sağlar.
* **Depolama hesabı anahtarı** , Web hizmeti ile ilişkilendirilmiş depolama hesabı anahtarı güncelleştirmenizi sağlar. 
* **Örnek verileri etkinleştirmek** istek-yanıt hizmeti test etmek için kullanabileceğiniz örnek verileri sağlamanıza izin verir. Machine Learning Studio'da web hizmeti oluşturduysanız, örnek verileri verilerden modelinizi eğitmek için kullanılan, alınır. Hizmet program aracılığıyla oluşturduysanız, verileri JSON paketinin bir parçası sağlanan örnek verileri alınır.

### <a name="managing-billing-plans"></a>Faturalandırma planları yönetme
Tıklatın **planları** web services hızlı başlangıç sayfasından menü seçeneği. Bu planı yönetmek için belirli Web hizmetiyle ilişkili planı tıklatabilirsiniz.

* **Yeni** yeni bir plan oluşturmanıza olanak sağlar.
* **Ekle/Kaldır Plan örneği** "Kapasite eklemek için var olan bir planı genişletilecek" sağlar.
* **Yükseltme/indirgeme** "Kapasite eklemek için var olan bir planı ölçeği" sağlar.
* **Silme** bir planı silmenize olanak sağlar.

Bir planı kendi panoyu görüntülemek için tıklatın. Pano belirli bir dönem anlık görüntü veya plan kullanım sağlar. Görüntülenecek zaman aralığını seçmek için tıklatın **süresi** Pano'nun sağ üst açılır. 

Plan Panosu aşağıdaki bilgileri sağlar:

* **Plan açıklaması** maliyetleri ve kapasite planla ilişkili hakkındaki bilgileri görüntüler.
* **Plan kullanım** işlemleri ve plan ücret işlem saatleri sayısını görüntüler.
* **Web Hizmetleri** bu planı kullanarak Web Hizmetleri sayısını görüntüler.
* **İlk olarak Web hizmeti çağrıları** plan ücretlendirilen çağrıları yapma üst dört Web hizmetleri görüntüler.
* **Web Hizmetleri tarafından işlem sa üst** plan ücretlendirilen işlem kaynakları kullanılarak üst dört Web hizmetleri görüntüler.

## <a name="manage-classic-web-services"></a>Klasik Web Hizmetleri yönetme
> [!NOTE]
> Bu bölümdeki yordamlar, Klasik web hizmetleri Azure Machine Learning Web Hizmetleri Portalı aracılığıyla yönetmek için uygundur. Machine Learning Studio ve klasik Azure Portalı aracılığıyla Klasik Web Hizmetleri yönetme hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning çalışma alanını yönetme](machine-learning-manage-workspace.md).
> 
> 

Klasik Web hizmetleri yönetmek için:

1. Oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) Microsoft Azure kullanarak portal hesabı - Azure aboneliğiyle ilişkili hesabı kullanın.
2. Menüsünde **Klasik Web Hizmetleri**.

Klasik Web hizmeti yönetmek için tıklatın **Klasik Web Hizmetleri**. Klasik Web Hizmetleri sayfasından şunları yapabilirsiniz:

* Web hizmeti ilişkili uç noktaları görüntülemek için tıklatın.
* Bir web hizmeti silin.

Klasik Web hizmeti yönetirken, her bitiş noktalarının ayrı olarak yönetin. Bir web hizmeti Web Hizmetleri sayfasında tıkladığınızda, hizmetle ilişkilendirilmiş uç noktaları listesi açılır. 

Klasik Web Hizmeti uç noktası sayfasında, eklemek ve hizmette uç noktalarını silin. Uç noktaları ekleme hakkında daha fazla bilgi için bkz: [uç noktaları oluşturma](machine-learning-create-endpoint.md).

Web hizmeti hızlı başlangıç sayfasını açmak için uç noktalar birini tıklatın. Hızlı Başlangıç sayfasında, web hizmetiniz yönetmenize olanak iki menü seçeneği vardır:

* **PANO** -Web hizmeti kullanım görüntülemenize izin verir.
* **Yapılandırma** - açıklayıcı metin eklemenize izin verir hata günlüğünü açıp kapatabilirsiniz, Web hizmeti ile ilişkilendirilmiş depolama hesabına ait anahtar güncelleştirir etkinleştirmek ve örnek verileri devre dışı bırakın.

### <a name="monitoring-how-the-web-service-is-being-used"></a>Web hizmeti nasıl kullanıldığını izleme
Tıklatın **PANO** sekmesi.

Panodan bir süre boyunca, Web hizmetinin genel kullanım görüntüleyebilirsiniz. Sağ üst köşesinde kullanım grafiklerini dönem açılır menüsünden görüntülemek için dönemi seçebilirsiniz. Pano aşağıdaki bilgileri gösterir:

* **Zaman içinde istekleri** seçilen süre boyunca bir adım grafiği isteklerinin sayısını görüntüler. Bu, kullanımında ani karşılaşıyorsanız tanımlamaya yardımcı olabilir.
* **İstek-yanıt istekleri** hizmet seçilen zaman aralığı ve bunlardan kaç tanesinin başarısız üzerinden aldı istek-yanıt çağrıları toplam sayısını gösterir.
* **Ortalama istek-yanıt işlem süresi** alınan isteklerin yürütülebilmesi için gereken süre ortalama görüntüler.
* **Toplu istekleri** Batch hizmeti, seçilen zaman aralığı ve bunlardan kaç tanesinin başarısız üzerinden aldı istek toplam sayısını gösterir.
* **Ortalama iş gecikme süresi** alınan isteklerin yürütülebilmesi için gereken süre ortalama görüntüler.
* **Hataları** web hizmeti çağrıları ortaya çıkan hataları toplam sayısını görüntüler.
* **Hizmetleri maliyetleri** fatura planı hizmetiyle ilişkili ücretleri görüntüler.

### <a name="configuring-the-web-service"></a>Web hizmetini yapılandırma
Tıklatın **yapılandırma** menü seçeneği.

Aşağıdaki özellikler güncelleştirebilirsiniz:

* **Açıklama** Web hizmeti için bir açıklama girmenize olanak sağlar. Açıklama gerekli bir alandır.
* **Günlük** etkinleştirmek veya devre dışı noktadaki günlüğü hata olanak tanır. Günlüğe kaydetme hakkında daha fazla bilgi için bkz [Machine Learning web hizmetleri için günlüğe kaydetme](machine-learning-web-services-logging.md).
* **Örnek verileri etkinleştirmek** istek-yanıt hizmeti test etmek için kullanabileceğiniz örnek verileri sağlamanıza izin verir. Machine Learning Studio'da web hizmeti oluşturduysanız, örnek verileri verilerden modelinizi eğitmek için kullanılan, alınır. Hizmet program aracılığıyla oluşturduysanız, verileri JSON paketinin bir parçası sağlanan örnek verileri alınır.

## <a name="grant-or-suspend-access-to-web-services-for-users-in-the-portal"></a>Vermek veya kullanıcılar için Web hizmetlerine erişim portalda askıya alma
Klasik Azure portalını kullanarak, belirli kullanıcılar için erişime veya izin verin.

### <a name="access-for-users-of-new-web-services"></a>Kullanıcılar yeni Web Hizmetleri için erişim
Diğer kullanıcıların Web hizmetlerinizi Azure Machine Learning Web Hizmetleri portalında çalışmak üzere etkinleştirmek için bunları ortak yöneticileri Azure aboneliğinize eklemeniz gerekir.

Oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Microsoft Azure kullanarak hesabı - Azure aboneliğiyle ilişkili hesabı kullanın.

1. Gezinti bölmesinde **ayarları**, ardından **Yöneticiler**.
2. Pencerenin alt kısmındaki tıklatın **Ekle**. 
3. Bir ortak yönetici Ekle iletişim kutusunda, ortak yönetici olarak ekleme ve erişmek için ortak yönetici istediğiniz aboneliği seçmek istediğiniz kişinin e-posta adresini yazın.
4. **Kaydet** düğmesine tıklayın.

### <a name="access-for-users-of-classic-web-services"></a>Klasik Web Hizmetleri kullanıcıları için erişim
Bir çalışma alanı yönetmek için:

Oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Microsoft Azure kullanarak hesabı - Azure aboneliğiyle ilişkili hesabı kullanın.

1. Microsoft Azure Hizmetleri panelinde tıklatın **MACHINE LEARNING**.
2. Yönetmek istediğiniz çalışma alanına tıklayın.
3. Tıklatın **yapılandırma** sekmesi.

Yapılandırma sekmesinden, Machine Learning çalışma alanına erişim tıklayarak askıya alabilirsiniz **REDDETME**. Kullanıcılar artık Machine Learning Studio'da çalışma alanını açın mümkün olacaktır. Erişimi geri yüklemek için **izin**.

Belirli kullanıcılar için:

Machine Learning Studio'da çalışma alanına erişimi olan ek hesapları yönetmek için tıklatın **oturum açma ML Studio** içinde **PANO** sekmesi. Bu çalışma alanı Machine Learning Studio'da açılır. Buradan, tıklatın **ayarları** sekmesini ve ardından **kullanıcılar**. Tıklayabilirsiniz **daha fazla kullanıcı davet** kullanıcılar için çalışma alanına erişim vermek veya bir kullanıcı seçin ve **kaldırmak**.

> [!NOTE]
> **Oturum açma ML Studio** bağlantısı, Machine Learning Studio, şu anda oturumunuz içine Microsoft Account kullanarak açar. Bir çalışma alanı oluşturmak için Klasik Azure portalında oturum açmak için kullandığınız Microsoft Account otomatik olarak bu çalışma alanını açmak için izni yok. Bir çalışma alanını açmak için çalışma alanı sahibi olarak tanımlandı Microsoft Account oturum açmanız gerekir veya çalışma alanına katılmaya sahibinden davet almak gerekir.
> 
> 

