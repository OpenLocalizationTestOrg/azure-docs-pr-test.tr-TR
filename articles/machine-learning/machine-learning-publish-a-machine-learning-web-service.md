---
title: bir Machine Learning web hizmeti aaaDeploy | Microsoft Docs
description: "Tooa Tahmine dayalı denemeye tooconvert eğitim denemeler nasıl dağıtım için hazırlamak ve ardından bir Azure Machine Learning web hizmeti olarak dağıtın."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 73a3e9c6-00d0-41d4-8cf1-2ec87713867e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9cb7af637632b2c3688c11483f29cf24df8fd065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a>Azure Machine Learning web hizmeti dağıtma
Azure Machine Learning toobuild sağlar, test ve Tahmine dayalı analitik çözümleri dağıtın.

Bir üst düzey noktası-in-görünümden, bu üç adımda gerçekleştirilir:

* **[Eğitim denemenizi oluşturma]**  -Azure Machine Learning Studio tootrain kullanın ve Tahmine dayalı bir analiz test işbirliği görsel geliştirme ortamı olduğundan, sağladığınız eğitim verilerini kullanarak modeli.
* **[Tooa Tahmine dayalı denemeye Dönüştür]**  - modelinizi var olan verilerle eğitilmiş ve hazır toouse olduğunuz sonra onu tooscore yeni verileri hazırlamak ve denemenizi Öngörüler için kolaylaştırmak.
* **[Web hizmeti olarak dağıtabilir]**  -Tahmine dayalı denemenizi olarak dağıttığınız bir [yeni] veya [Klasik] Azure web hizmeti. Kullanıcıların veri tooyour modeli gönderip modelinizin tahminleri alabilirsiniz.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a>Eğitim denemenizi oluşturma
tootrain bir Tahmine dayalı bir analiz modeli, Azure Machine Learning Studio'da toocreate Burada, çeşitli modülleri tooload eğitim verileri dahil etmek, hello verileri gereken şekilde hazırlayın, machine learning algoritmaları uygulamak ve hello sonuçları değerlendirin eğitim denemenizi kullanın . Bir deneme üzerinde yinelemek ve farklı makine öğrenimi algoritmaları toocompare deneyin ve hello sonuçları değerlendirin.

oluşturma ve eğitim denemeler yönetme hello sürecini daha kapsamlı başka bir yere ele alınmıştır. Daha fazla bilgi için bu makalelere bakın:

* [Azure Machine Learning Studio'da basit bir deneme oluşturma](machine-learning-create-experiment.md)
* [Azure Machine Learning ile Tahmine dayalı bir çözüm geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)
* [Azure Machine Learning Studio'ya eğitim verilerinizi alın](machine-learning-data-science-import-data.md)
* [Azure Machine Learning Studio'da deneme yinelemelerini yönetme](machine-learning-manage-experiment-iterations.md)

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Merhaba eğitim deneme tooa Tahmine dayalı denemeye Dönüştür
Modelinizi eğittiğimize sonra eğitim denemeler bir tahmini deneme tooscore yeni verilere hazır tooconvert demektir.

Tahmine dayalı tooa dönüştürerek denemeler, Puanlama bir web hizmeti olarak dağıtılmış, eğitilen model hazır toobe alıyorsunuz. Merhaba web hizmetinin kullanıcılar, giriş veri tooyour modeli ve modelinizi geri hello tahmin sonuçlarını gönderir gönderebilir. Dönüştürdüğünüz gibi tooa Tahmine dayalı denemeler, başkaları tarafından kullanılan, model toobe nasıl beklediğiniz göz önünde bulundurun.

tooconvert Tahmine dayalı, eğitim deneme tooa denemeler, tıklatın **çalıştırmak** hello deneme tuvalinin hello altındaki tıklatın **Web hizmetinin ayarı**seçeneğini belirleyip **Tahmine dayalı Web hizmeti** .

![Tooscoring deneme Dönüştür](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

Hakkında daha fazla bilgi için tooperform bu dönüştürme bkz [nasıl tooprepare modelinizi Azure Machine Learning Studio'daki dağıtımı için](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Merhaba aşağıdaki adımlar bir tahmini deneme yeni bir web hizmeti olarak dağıtma açıklar. Merhaba deneme Klasik web hizmeti olarak da dağıtabilirsiniz.

## <a name="deploy-it-as-a-web-service"></a>Bir web hizmeti olarak dağıtma

Merhaba Tahmine dayalı denemeye yeni bir web hizmeti veya bir Klasik web hizmeti olarak dağıtabilirsiniz.

### <a name="deploy-hello-predictive-experiment-as-a-new-web-service"></a>Yeni bir web hizmeti olarak Hello tahmini deneme dağıtma
Merhaba Tahmine dayalı denemeye hazır, yeni bir Azure web hizmeti olarak dağıtabilirsiniz. Merhaba web hizmetini kullanarak, kullanıcılar veri tooyour modeli gönderebilir ve hello modeli kendi tahminleri döndürür.

toodeploy, Tahmine dayalı denemeler, tıklatın **çalıştırmak** tuvale hello hello sonunda deneme. Merhaba deneme çalışması bittikten sonra tıklayın **Web hizmeti Dağıt** seçip **Web hizmeti Dağıt [yeni]**.  Merhaba Machine Learning Web hizmeti portal Hello dağıtım sayfasını açar.

> [!NOTE] 
> toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir. Daha fazla bilgi için [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md). 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a>Machine Learning Web hizmeti portal dağıtma deneme sayfası
Merhaba dağıtmak deneme sayfasında hello web hizmeti için bir ad girin.
Fiyatlandırma planı seçin. Aksi takdirde, seçebilirsiniz varolan bir fiyatlandırma planı varsa, hello hizmet için yeni bir fiyat planı oluşturmanız gerekir.

1. Merhaba, **fiyat planı** açılan, var olan bir planı veya seçin hello **Select yeni plan** seçeneği.
2. İçinde **Plan adı**, faturanızı hello planına tanımlayacak bir ad yazın.
3. Merhaba birini **aylık Plan katmanlarını**. Katmanları toohello planları varsayılan bölgeniz ve web hizmetiniz için varsayılan hello planı dağıtılan toothat bölgedir.

Tıklatın **dağıtma** ve hello **Hızlı Başlangıç** web hizmetiniz için sayfası açılır.

Hello web hizmeti hızlı başlangıç sayfası hello en yaygın görevler, bir web hizmeti oluşturduktan sonra gerçekleştireceksiniz erişim ve rehberlik sağlar. Buradan, hello Test sayfası ve Tüket sayfası kolayca erişebilirsiniz.

<!-- ![Deploy hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a>Yeni web hizmetinizi test
tootest yeni web hizmetinizi tıklatın **Test web hizmeti** Ortak Görevler'in altında. Merhaba Test sayfasında, web hizmetiniz bir istek-yanıt hizmeti'olarak (RR) veya toplu iş yürütme hizmeti (BES) test edebilirsiniz.

Merhaba RRS test sayfası hello giriş, çıkış ve hello deneme için tanımladığınız genel parametreleri görüntüler. tootest hello web hizmeti, el ile uygun değerleri hello girişleri veya kaynağı için hello test değerlerini içeren bir virgülle ayrılmış değer (CSV) biçimlendirilmiş bir dosya girebilirsiniz.

RRS, kullanarak tootest hello liste görünümü modundan hello girişleri için uygun değerleri girin ve tıklayın **Test istek-yanıt**. Tahmin sonuçlarınızı hello çıkış sütunu toohello sol içinde görüntüler.

![Merhaba web hizmetini dağıtma](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

tootest, BES tıklatın **toplu**. Merhaba toplu test sayfasında girişinizi altında Gözat'ı tıklatın ve uygun örnek değerler içeren bir CSV dosyası seçin. Bir CSV dosyası yok ve Machine Learning Studio kullanarak Tahmine dayalı denemenizi oluşturulan, hello veri kümesi için Tahmine dayalı denemenizi indirin ve kullanın.

toodownload hello veri kümesi, açık Machine Learning Studio. Tahmine dayalı denemenizi açın ve denemeniz için giriş hello sağ tıklayın. Merhaba bağlam menüsünden seçin **dataset** ve ardından **karşıdan**.

![Merhaba web hizmetini dağıtma](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

Tıklatın **Test**. Toplu iş yürütme işinizi Hello durumunu görüntüler toohello sağ altında **Test toplu işlerini**.

![Merhaba web hizmetini dağıtma](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

Merhaba üzerinde **yapılandırma** sayfasında, hello açıklamasını değiştirmek, başlık, güncelleştirme hello depolama hesabı anahtarı ve web hizmetiniz için örnek verileri etkinleştirin.

![Merhaba web hizmetini yapılandır](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

Merhaba web hizmeti dağıttıktan sonra sonra şunları yapabilirsiniz:

* **Erişim** hello web hizmeti API'si üzerinden.
* **Yönetme** üzerinden Azure Machine Learning web hizmetleri portalı veya Klasik Azure portalı hello.
* **Güncelleştirme** , modelinizi değişirse.

#### <a name="access-your-new-web-service"></a>Yeni web hizmetine erişim
Machine Learning Studio'dan web hizmetini dağıttığınızda, veri toohello hizmeti gönderip yanıtları programlı olarak alabilirsiniz.

Merhaba **Tüket** sayfası, web hizmetiniz tooaccess gereken tüm hello bilgileri sağlar. Örneğin, hello API anahtarı yetkili tooallow erişim toohello hizmeti sağlanır.

Machine Learning web hizmetine erişim hakkında daha fazla bilgi için bkz: [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).

#### <a name="manage-your-new-web-service"></a>Yeni web hizmetinizi yönetme
Yeni web hizmetleri Machine Learning Web Hizmetleri portalı yönetebilirsiniz. Merhaba gelen [ana portal sayfası](https://services.azureml-test.net/), tıklatın **Web Hizmetleri**. Merhaba web Hizmetleri sayfasından silin veya bir hizmet kopyalayın. belirli bir hizmeti toomonitor hello hizmete tıklayın ve ardından **Pano**. Merhaba web hizmetiyle ilişkili toomonitor toplu işleri tıklatın **toplu isteği günlük**.

### <a name="deploy-hello-predictive-experiment-as-a-classic-web-service"></a>Merhaba Tahmine dayalı denemeye Klasik web hizmeti olarak dağıtma

Merhaba Tahmine dayalı denemeye yeterince hazırlandı, Klasik Azure web hizmeti olarak dağıtabilirsiniz. Merhaba web hizmetini kullanarak, kullanıcılar veri tooyour modeli gönderebilir ve hello modeli kendi tahminleri döndürür.

toodeploy, Tahmine dayalı denemeler, tıklatın **çalıştırmak** hello hello altındaki tuvale deneyin ve ardından **Web hizmeti Dağıt**. Merhaba web hizmeti ayarlayın ve hello web hizmeti panosunda yerleştirilir.

![Merhaba web hizmetini dağıtma](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a>Klasik web hizmeti test etme

Merhaba Machine Learning Web Hizmetleri portalı veya Machine Learning Studio hello web hizmetini test edebilirsiniz.

tootest hello istek yanıtı web hizmeti, tıklatın hello **Test** hello web hizmeti panosunda düğmesi. Bir iletişim tooask, hello hizmeti için bir giriş verisi hello açılır. Bu deneme Puanlama hello tarafından beklenen hello sütunlar'dır. Bir veri kümesi girin ve ardından **Tamam**. Merhaba web hizmeti tarafından oluşturulan hello sonuçları hello Pano hello altında görüntülenir.

Merhaba tıklayabilirsiniz **Test** hello yeni web hizmeti bölümünde daha önce gösterildiği gibi bağlantı tootest hizmetinizi hello Azure Machine Learning Web Hizmetleri portalında Önizleme.

tootest hello toplu yürütme hizmeti,'ı tıklatın **Test** Önizleme bağlantı. Merhaba toplu test sayfasında girişinizi altında Gözat'ı tıklatın ve uygun örnek değerler içeren bir CSV dosyası seçin. Bir CSV dosyası yok ve Machine Learning Studio kullanarak Tahmine dayalı denemenizi oluşturulan, hello veri kümesi için Tahmine dayalı denemenizi indirin ve kullanın.

![Test hello web hizmeti](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

Merhaba üzerinde **yapılandırma** sayfasında hello hizmetin hello görünen adını değiştirebilir ve bir açıklama girin. Merhaba ad ve açıklama hello görüntülenen [Klasik Azure portalı](http://manage.windowsazure.com/) web hizmetlerinizi yöneteceğiniz.

Bir açıklama giriş verileri, çıktı verilerini ve web hizmeti parametreleri altında her sütun için bir dize girerek sağlayabilirsiniz **giriş ŞEMASINI**, **çıkış ŞEMASI**, ve **Web hizmeti PARAMETRE**. Bu açıklamalar hello web hizmeti için sağlanan hello örnek kodu belgelerinde kullanılır.

Web hizmetiniz erişildiğinde görüyorsunuz hatalar günlük toodiagnose etkinleştirebilirsiniz. Daha fazla bilgi için bkz: [Machine Learning web hizmetleri için günlüğe kaydetmeyi etkinleştirmek](machine-learning-web-services-logging.md).

![Merhaba web hizmetini yapılandır](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

Ayrıca, hello hello yeni web hizmeti bölümünde daha önce gösterilen Azure Machine Learning Web Hizmetleri portalı benzer toohello yordamı hello uç noktaları hello web hizmeti için de yapılandırabilirsiniz. Başlangıç seçenekleri farklıdır, ekleyebilir veya hello hizmet açıklaması, etkinleştirme günlüğe kaydetme ve test etmek için etkinleştir örnek verileri değiştirebilirsiniz.

#### <a name="access-your-classic-web-service"></a>Klasik web hizmetine erişim
Machine Learning Studio'dan web hizmetini dağıttığınızda, veri toohello hizmeti gönderip yanıtları programlı olarak alabilirsiniz.

Hello Pano web hizmetiniz tooaccess gereken tüm hello bilgileri sağlar. Örneğin, erişim toohello hizmeti tooallow yetkili ve API yardım sayfalarına kodunuzu yazmaya başlamak toohelp sağlanan hello API anahtarı bulunur.

Machine Learning web hizmetine erişim hakkında daha fazla bilgi için bkz: [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).

#### <a name="manage-your-classic-web-service"></a>Klasik web hizmetinizi yönetme
Vardır çeşitli eylemleri toomonitor bir web hizmeti gerçekleştirebilirsiniz. Güncelleştirin ve silin. Ek uç noktaları tooa Klasik web hizmeti, dağıttığınızda oluşturduğunuz ek toohello varsayılan uç noktası da ekleyebilirsiniz.

Daha fazla bilgi için bkz: [bir Azure Machine Learning çalışma alanını yönetme](machine-learning-manage-workspace.md) ve [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir web hizmeti yönetmek](machine-learning-manage-new-webservice.md).

<!-- When this article gets published, fix hello link and uncomment
For more information on how toomanage Azure Machine Learning web service endpoints using hello REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-hello-web-service"></a>Merhaba web hizmetini güncelleştirmek
Ek eğitim verilerle hello modeli güncelleştirme gibi tooyour web hizmeti, değişiklikleri yapın ve tekrar, hello özgün web hizmeti üzerine dağıtın.

tooupdate hello web hizmeti açın hello özgün Tahmine dayalı denemeye toodeploy hello web hizmeti kullanılan ve tıklayarak düzenlenebilir bir kopya yapmak **SAVE AS**. İstediğiniz değişiklikleri yapın ve ardından **Web hizmeti Dağıt**.

Bu deneme önce dağıttıktan sonra çünkü toooverwrite (Klasik Web hizmeti) veya güncelleştirme (Yeni web hizmeti) hello varolan hizmet isteyip istemediğinizi istenir. Tıklatarak **Evet** veya **güncelleştirme** hello varolan web hizmetini durdurur ve dağıtır hello yeni Tahmine dayalı denemeye onun yerine dağıtılır.

> [!NOTE]
> Yapılandırma değişiklikleri hello özgün web hizmetinde yaptıysanız, örneğin, yeni bir görünen ad veya açıklama girme, tooenter bu değerleri yeniden gerekir.
> 
> 

Web hizmeti güncelleştirmek için bir seçenek tooretrain hello program aracılığıyla modelidir. Daha fazla bilgi için bkz. [Machine Learning modellerini programlama aracılığıyla yeniden eğitme](machine-learning-retrain-models-programmatically.md).

<!-- internal links -->
[Eğitim denemenizi oluşturma]: #create-a-training-experiment
[Tooa Tahmine dayalı denemeye Dönüştür]: #convert-the-training-experiment-to-a-predictive-experiment
[Web hizmeti olarak dağıtabilir]: #deploy-it-as-a-web-service
[yeni]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Klasik]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
