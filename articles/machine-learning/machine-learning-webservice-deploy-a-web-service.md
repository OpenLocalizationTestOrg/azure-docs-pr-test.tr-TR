---
title: Yeni bir web hizmeti Azure Machine learning'de aaaDeploying | Microsoft Docs
description: "web hizmeti bir ARM dağıtma hello iş akışı tabanlı"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a>Yeni bir web hizmeti dağıtma
Microsoft Azure Machine şimdi learning temel alan web hizmetleri sağlar [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) yeni faturalama planı seçeneklerini ve web hizmeti toomultiple bölgeler dağıtma için izin verme.

Merhaba genel iş akışı toodeploy Microsoft Azure Machine Learning Web Hizmetleri kullanarak bir web hizmeti aşağıdaki gibidir:

* Tahmine dayalı bir deneme oluşturma
* dağıtın
* kendi adı yapılandırma
* Fatura planı
* test
* Bunu kullanabilir.

Grafiği aşağıdaki hello hello iş akışı gösterilmiştir.

![Web hizmeti dağıtım iş akışı][1]

## <a name="deploy-web-service-from-studio"></a>Studio'dan Web hizmetini dağıtma
bir deneme yeni bir web hizmeti olarak toodeploy. Machine Learning Studio Hello oturum açın ve yeni bir Tahmine dayalı web hizmeti oluşturun. 

**Not**: Klasik web hizmeti olarak bir deneme zaten dağıttıysanız, yeni bir web hizmeti olarak dağıtamazsınız.

Tıklatın **çalıştırmak** hello hello altındaki tuvale deneyin ve ardından **Web hizmeti Dağıt** ve **Web hizmeti dağıtma [Yeni]**. Merhaba Machine Learning Web Hizmeti Yöneticisi'nin Hello dağıtım sayfasını açar.

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a>Machine Learning Web Hizmeti Yöneticisi'ni dağıtmak deneme sayfası
Merhaba dağıtmak deneme sayfasında hello web hizmeti için bir ad girin.
Fiyatlandırma planı seçin. Aksi takdirde, seçebilirsiniz varolan bir fiyatlandırma planı varsa, hello hizmet için yeni bir fiyat planı oluşturmanız gerekir. 

1. Merhaba, **fiyat planı** açılan, var olan bir planı veya seçin hello **Select yeni plan** seçeneği.
2. İçinde **Plan adı**, faturanızı hello planına tanımlayacak bir ad yazın.
3. Merhaba birini **aylık Plan katmanlarını**. Merhaba plan katmanlarını toohello planları varsayılan bölgeniz ve web hizmetiniz için varsayılan not dağıtılan toothat bölgedir.

Tıklatın **dağıtma** ve web hizmetiniz için hello hızlı başlangıç sayfasını açar.

## <a name="quickstart-page"></a>Hızlı Başlangıç sayfası
Hello web hizmeti hızlı başlangıç sayfası yeni bir web hizmeti oluşturduktan sonra gerçekleştirecek hello en yaygın görevleri erişim ve rehberlik sağlar. Buradan hem hello kolayca erişebilirsiniz **Test** sayfa ve **Tüket** sayfası.

## <a name="testing-your-web-service"></a>Web hizmeti test etme
Merhaba hızlı başlangıç sayfası, Ortak Görevler altında Test web hizmeti tıklayın.   

tootest hello web hizmeti bir istek-yanıt hizmeti'olarak (RR):

* Tıklatın **Test** hello menü çubuğunda.
* Tıklatın **istek-yanıt**.
* Merhaba giriş sütunlarının denemenizi için uygun değerleri girin.
* Test tıklatın **istek-yanıt**.

Merhaba sağ tarafta hello sayfasının, sonuçları görüntüler.

tootest toplu yürütme hizmeti (BES) web hizmeti, bir CSV dosyası kullanır:

* Tıklatın **Test** hello menü çubuğunda.
* Tıklatın **toplu**.
* Giriş altında Gözat'ı tıklatın ve tooyour örnek veri dosyası gidin.
* Tıklatın **Test**.

test Hello durumunu altında görüntülenen **Test toplu işleri**.

## <a name="consuming-your-web-service"></a>Web hizmetini kullanma
Bir web hizmeti olarak dağıtıldığında, Azure Machine Learning denemeleri çok çeşitli aygıtlar ve platformlar tarafından kullanılabilecek bir REST API sağlar. İletileri basit REST API kabul eder ve JSON ile yanıt verir Merhaba biçimlendirilmiş olmasıdır. Hello Azure Machine Learning portal sağlar kullanılabilir kod toocall hello web hizmeti R, C# ve Python.

Merhaba tüketim sayfasında bulabilirsiniz:

* Merhaba API anahtarı ve web hizmeti uygulamalarda tüketimi için URI'si.
* Excel ve web uygulama şablonları tookick tüketim işlemi başlatın.
* C#, python ve R tooget örnek kodda, başlatıldı.

Web hizmetleri kullanma ile ilgili daha fazla bilgi için bkz: [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).

## <a name="next-steps"></a>Sonraki Adımlar
Web hizmetleri kullanma ile ilgili daha fazla bilgi için bkz:

[Nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md)

[Azure Machine Learning Web Hizmetleri: Dağıtım ve kullanım](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
