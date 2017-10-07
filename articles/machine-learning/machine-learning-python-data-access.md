---
title: "Machine Learning Python istemci kitaplığı aaaAccess kümeleriyle | Microsoft Docs"
description: "Yükleme ve hello Python istemci kitaplığı tooaccess kullanın ve Azure Machine Learning veri güvenli bir şekilde bir yerel Python ortamınızdan yönetin."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a>Python hello Azure Machine Learning Python istemci kitaplığı kullanılarak erişim kümeleriyle
Microsoft Azure Machine Learning Python istemci kitaplığı Hello önizlemesini güvenli erişim tooyour Azure Machine Learning veri kümelerini yerel Python Ortamı'ndan etkinleştirebilir ve hello oluşturulmasını ve bir çalışma alanı kümelerinde yönetimini sağlar.

Bu konu hakkında yönergeler sağlar:

* Merhaba Machine Learning Python istemci Kitaplığı'nı yüklemek 
* erişim ve yönergeler de dahil olmak üzere veri kümeleri, karşıya yükleme tooget yetkilendirme tooaccess, yerel Python ortamınızdan Azure Machine Learning veri kümeleri
* denemeler ara veri kümeleri erişim
* Merhaba Python istemci kitaplığı tooenumerate veri kümelerini kullanan, meta verilerine erişmek, bir veri kümesi hello içeriğini okumak, yeni veri kümeleri oluşturma ve mevcut veri kümelerini güncelleştirme

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="prerequisites"></a>Önkoşullar
Merhaba Python istemci kitaplığı ortamları aşağıdaki hello altında test edilmiştir:

* Windows, Mac ve Linux
* Python 2.7, 3.3 ve 3.4

Bu paketleri aşağıdaki hello üzerinde bir bağımlılığa sahiptir:

* istekleri
* Python dateutil
* pandas

Bir Python dağıtımı gibi kullanmanızı öneririz [Anaconda](http://continuum.io/downloads#all) veya [Kanopi](https://store.enthought.com/downloads/), Python, IPython gelen ve yukarıda listelenen hello üç paketleri yüklü. IPython kesinlikle gerekli olmamakla birlikte, düzenleme ve etkileşimli olarak verileri görselleştirmek için harika bir ortamıdır.

### <a name="installation"></a>Nasıl tooinstall hello Azure Machine Learning Python istemci kitaplığı
Hello Azure Machine Learning Python istemci kitaplığı da yüklü toocomplete hello görevleri bu konuda anlatılan olması gerekir. Hello kullanılabilir [Python paket dizini](https://pypi.python.org/pypi/azureml). tooinstall Python ortamınızda çalışması hello aşağıdaki komut, yerel Python ortamınızdan:

    pip install azureml

Alternatif olarak, indirin ve hello kaynaklardan yüklemek [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).

    python setup.py install

Makinenizde git varsa, doğrudan hello git deposundan PIP tooinstall kullanabilirsiniz:

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <a name="datasetAccess"></a>Studio kod parçacıkları tooaccess veri kümelerini kullanma
Merhaba Python istemci kitaplığı çalıştırılmış denemeler programlı erişim tooyour mevcut veri kümeleri sağlar.

Merhaba Studio web arabiriminden konumu makinenizde Pandas DataFrame nesne olarak seri durumdan veri kümeleri ve tüm hello gerekli bilgileri toodownload içeren kod parçacıkları oluşturabilir.

### <a name="security"></a>Veri erişimi için güvenlik
kod parçacıkları hello Python istemci kitaplığı ile kullanmak üzere çalışma alanı kimliği ve yetkilendirme içerir Studio tarafından sağlanan hello belirteci. Bunlar tam erişim tooyour çalışma sağlayın ve parola gibi korunmalıdır.

Güvenlik nedenleriyle hello kod parçacığı işlevleri olarak ayarlayın, rolde kullanılabilir toousers Only'dir **sahibi** hello çalışma alanı için. Rolünüze üzerinde hello Azure Machine Learning Studio'da görüntülenir **kullanıcılar** altında sayfa **ayarları**.

![Güvenlik][security]

Rolünüze olarak ayarlanmamışsa **sahibi**, istek sahibi olarak ortamına yeniden davet toobe veya hello çalışma tooprovide hello sahibi isteyin hello kod parçacığını sizinle.

tooobtain hello yetkilendirme belirtecini hello aşağıdakilerden birini yapabilirsiniz:

* Bir belirteci için bir sahibinden isteyin. Sahipleri kendi yetkilendirme belirteçleri Studio'da kendi çalışma alanının hello Ayarları sayfasından erişebilirsiniz. Seçin **ayarları** sol bölmesinde ve tıklatın hello gelen **YETKİLENDİRME BELİRTEÇLERİ** toosee hello birincil ve ikincil belirteçleri.  Hello birincil veya ikincil yetkilendirme belirteçleri hello hello kod parçacığında kullanılabilse de sahipleri yalnızca hello ikincil yetkilendirme belirteçleri paylaşıma önerilir.

![Yetkilendirme belirteçleri](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* Yükseltilen toobe toorole sahibinin isteyin.  toodo bu hello çalışma gereksinimlerini toofirst geçerli sahibini hello çalışma alanından kaldırmak daha sonra yeniden davet tooit sahibi olarak.

Geliştiriciler hello çalışma alanı kimliği ve yetkilendirme aldıktan sonra rolleri bakılmaksızın hello kod parçacığını kullanarak mümkün tooaccess hello çalışma oldukları belirteç.

Yetkilendirme belirteçleri hello üzerinde yönetilen **YETKİLENDİRME BELİRTEÇLERİ** altında sayfa **ayarları**. Bunları yeniden oluşturabilirsiniz, ancak bu yordamı erişim toohello önceki belirteci iptal eder.

### <a name="accessingDatasets"></a>Yerel bir Python uygulama erişim veri kümeleri
1. Machine Learning Studio'da tıklatın **veri KÜMELERİ** hello sol gezinti çubuğunda hello.
2. Tooaccess istediğiniz hello veri kümesi seçin. Hello hello veri kümelerini seçebilirsiniz **MY veri KÜMELERİ** listesi veya hello **örnekleri** listesi.
3. Merhaba alt araç çubuğundan tıklatın **veri erişim kodu oluştur**. Merhaba veri hello Python istemci kitaplığı ile uyumlu bir biçimde ise, bu düğmesi devre dışıdır.
   
    ![Veri kümeleri][datasets]
4. Merhaba kod parçacığını görünür hello penceresinden seçin ve tooyour panoya kopyalayın.
   
    ![Erişim kodu][dataset-access-code]
5. Merhaba kodu yerel Python uygulamanızı hello not defterinize yapıştırın.
   
    ![Not Defteri][ipython-dataset]

## <a name="accessingIntermediateDatasets"></a>Machine Learning denemelerini ara veri kümeleri erişim
Bir denemeyi Machine Learning Studio hello çalıştırıldıktan sonra olası tooaccess modüllerin hello çıkış düğümlerinden hello ara veri kümeleri var. Ara veri kümeleri oluşturulan ve model aracı çalıştırdığınızda ara adımlar için kullanılan verilerdir.

Merhaba veri biçimi hello Python istemci kitaplığı ile uyumlu olduğu sürece ara veri kümeleri erişilebilir.

Merhaba aşağıdaki biçimleri desteklenir (sabittir bu hello `azureml.DataTypeIds` sınıfı):

* Düz metin
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

Modül çıkış düğüm üzerinde gelerek hello biçimi belirleyebilirsiniz. Merhaba düğüm adı, bir araç ipucu ile birlikte görüntülenir.

Bazı hello gibi hello modüllerin [bölünmüş] [ split] modülü, çıktı tooa biçimi adlı `Dataset`, hello Python istemci kitaplığı tarafından desteklenmiyor.

![Veri kümesi biçimi][dataset-format]

Toouse dönüştürme modülü gibi gereken [Dönüştür tooCSV][convert-to-csv], tooget desteklenen bir biçime bir çıktı.

![GenericCSV biçimi][csv-format]

Merhaba aşağıdaki adımlar, bir deneme oluşturur, çalıştırır ve hello Ara dataset erişen bir örnek gösterir.

1. Yeni bir deneme oluşturun.
2. INSERT bir **yetişkin Census gelir ikili sınıflandırma dataset** modülü.
3. INSERT bir [bölünmüş] [ split] modül ve giriş toohello dataset modülü çıktısını bağlanın.
4. INSERT bir [Dönüştür tooCSV] [ convert-to-csv] modülü ve kendi giriş tooone Merhaba, bağlanmak [bölünmüş] [ split] modülü çıkarır.
5. Merhaba deneme kaydetmek, çalıştırmak ve bekleyin çalıştıran toofinish.
6. Merhaba Hello çıkış düğümüne tıklayın [Dönüştür tooCSV] [ convert-to-csv] modülü.
7. Merhaba bağlam menüsü görüntülendiğinde seçin **veri erişim kodu oluştur**.
   
    ![Bağlam menüsü][experiment]
8. Merhaba kod parçacığını seçin ve görüntülenen hello penceresinden tooyour panoya kopyalayın.
   
    ![Erişim kodu][intermediate-dataset-access-code]
9. Merhaba kodu defterinizde yapıştırın.
   
    ![Not Defteri][ipython-intermediate-dataset]
10. Matplotlib kullanarak hello veri görselleştirebilirsiniz. Bu hello yaş sütunu için bir histogram görüntüler:
    
    ![Çubuk grafik][ipython-histogram]

## <a name="clientApis"></a>Merhaba Machine Learning Python istemci kitaplığı tooaccess kullanın, okuma, oluşturma ve veri kümelerini yönetme
### <a name="workspace"></a>Çalışma alanı
Merhaba çalışma hello için giriş hello Python istemci kitaplığı noktasıdır. Merhaba sağlamak `Workspace` , çalışma alanı kimliği ve yetkilendirme belirteci toocreate ile sınıfının bir örneği:

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a>Veri kümeleri listeleme
tooenumerate belirli bir çalışma alanındaki tüm veri kümeleri:

    for ds in ws.datasets:
        print(ds.name)

tooenumerate yalnızca hello veri kümeleri kullanıcı oluşturuldu:

    for ds in ws.user_datasets:
        print(ds.name)

tooenumerate yalnızca hello örnek veri kümeleri:

    for ds in ws.example_datasets:
        print(ds.name)

Bir veri kümesi (büyük küçük harfe duyarlı) adı tarafından erişebilirsiniz:

    ds = ws.datasets['my dataset name']

Ya da dizin tarafından erişebilirsiniz:

    ds = ws.datasets[0]


### <a name="metadata"></a>Meta Veriler
Veri kümeleri meta verileri, toplama toocontent sahip. (Ara veri kümelerini bir özel durum toothis kuralı olan ve meta verileri yok.)

Bazı meta veri değerlerinin hello kullanıcı tarafından oluşturma sırasında atanır:

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

Başkaları tarafından Azure ML atanan değerler şunlardır:

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

Merhaba bkz `SourceDataset` sınıfı üzerinde daha fazla hello kullanılabilir meta veriler için.

### <a name="read-contents"></a>İçeriğini okuma
Machine Learning Studio tarafından otomatik olarak sağlanan hello kod parçacıkları indirin ve hello dataset tooa Pandas DataFrame nesne seri durumdan. Bu hello ile yapılır `to_dataframe` yöntemi:

    frame = ds.to_dataframe()

Toodownload hello ham verileri tercih ve hello seri durumdan çıkarma kendiniz gerçekleştirmek istiyorsanız, bir seçenek olmasıdır. Merhaba şu anda 'ARFF' hangi hello Python istemci kitaplığı seri durumdan çıkarılamıyor, gibi biçimler için hello tek seçenek budur.

metin olarak tooread hello içeriği:

    text_data = ds.read_as_text()

tooread hello içeriğini ikili olarak:

    binary_data = ds.read_as_binary()

Ayrıca bir akış toohello içeriği açabilirsiniz:

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a>Yeni bir veri kümesi oluşturma
Merhaba Python istemci kitaplığı Python programınızdan tooupload veri kümeleri sağlar. Bu veri kümeleri sonra çalışma alanınızda kullanılabilir.

Bir Pandas DataFrame verileriniz varsa, kodu aşağıdaki hello kullan:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

Verilerinizi zaten serileştirilmiş, kullanabilirsiniz:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

Merhaba Python istemci Pandas DataFrame toohello aşağıdaki biçimler mümkün tooserialize kitaplığıdır (sabittir bu hello `azureml.DataTypeIds` sınıfı):

* Düz metin
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

### <a name="update-an-existing-dataset"></a>Mevcut bir veri kümesini güncelleştir
Tooupload var olan bir dataset eşleşen bir ada sahip yeni bir veri kümesi çalışırsanız, bir çakışma hatası almanız gerekir.

var olan bir dataset tooupdate, önce tooget bir başvuru toohello mevcut veri kümesini gerekir:

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Ardından `update_from_dataframe` azure'da hello dataset tooserialize ve Değiştir hello içeriğini:

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Tooserialize hello veri tooa farklı biçimi istiyorsanız, isteğe bağlı hello için bir değer belirtin `data_type_id` parametresi.

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Hello için bir değer belirterek isteğe bağlı olarak yeni bir açıklama ayarlayabilirsiniz `description` parametresi.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

İsteğe bağlı olarak yeni bir ad hello için bir değer belirterek ayarlayabileceğiniz `name` parametresi. Şu andan itibaren yalnızca yeni adı hello kullanarak hello dataset almak. koddan hello hello verileri, ad ve açıklama güncelleştirir.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

Merhaba `data_type_id`, `name` ve `description` parametreler isteğe bağlıdır ve varsayılan tootheir önceki değer. Merhaba `dataframe` parametresi gereklidir her zaman.

Verilerinizi zaten serileştirilmiş kullanırsanız `update_from_raw_data` yerine `update_from_dataframe`. Yalnızca içinde geçirirseniz `raw_data` yerine `dataframe`, benzer şekilde çalışır.

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

