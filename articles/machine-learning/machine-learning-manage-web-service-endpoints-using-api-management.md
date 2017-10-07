---
title: "toomanage AzureML web hizmetleri API Management kullanarak nasıl aaaLearn | Microsoft Docs"
description: "Toomanage AzureML web API Management kullanarak hizmetleri nasıl gösteren bir kılavuzdur."
keywords: "machine Learning, API Yönetimi"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a>Toomanage AzureML web API Management kullanarak hizmetleri nasıl öğrenin
## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl gösterir tooquickly API Management toomanage AzureML web hizmetlerinizi kullanımına başlamanıza.

## <a name="what-is-azure-api-management"></a>Azure API Management nedir?
Azure API Management REST API uç noktalarınızı kullanıcı erişimi, kullanım azaltma ve Pano izleme tanımlayarak yönetmenizi sağlayan bir Azure hizmetidir. Tıklatın [burada](https://azure.microsoft.com/services/api-management/) Azure API Management hakkında ayrıntılı bilgi için. Tıklatın [burada](../api-management/api-management-get-started.md) tooget Azure API Management ile çalışmaya nasıl üzerinde Kılavuzu. Bu kılavuz temel alır, bu diğer Kılavuzu, ürünler, geliştirici abonelikleri ve kullanım dashboarding oluşturma bildirim yapılandırmaları, fiyatlandırma katmanı, yanıt işleme, kullanıcı kimlik doğrulaması dahil olmak üzere daha fazla konuları kapsar.

## <a name="what-is-azureml"></a>AzureML nedir?
AzureML tooeasily yapı sağlayan machine learning için bir Azure hizmetidir, dağıtmak ve Gelişmiş analiz çözümleri paylaşın. Tıklatın [burada](https://azure.microsoft.com/services/machine-learning/) AzureML hakkında ayrıntılı bilgi için.

## <a name="prerequisites"></a>Ön koşullar
toocomplete bu kılavuz, gerekir:

* Bir Azure hesabı. Bir Azure hesabınız yoksa tıklatın [burada](https://azure.microsoft.com/pricing/free-trial/) hakkında ayrıntılar için toocreate ücretsiz bir deneme hesabı.
* AzureML hesaptır. AzureML hesabınız yoksa tıklatın [burada](https://studio.azureml.net/) hakkında ayrıntılar için toocreate ücretsiz bir deneme hesabı.
* Hello çalışma alanı, hizmet ve bir web hizmeti olarak dağıtılan bir AzureML deneme apı_key. Tıklatın [burada](machine-learning-create-experiment.md) nasıl toocreate bir AzureML denemeler hakkında bilgi. Tıklatın [burada](machine-learning-publish-a-machine-learning-web-service.md) nasıl toodeploy bir AzureML denemeler bir web hizmeti olarak hakkında bilgi. Alternatif olarak, ek A nasıl toocreate ve test basit AzureML deneyin ve bir web hizmeti olarak dağıtmak için yönergeler içerir.

## <a name="create-an-api-management-instance"></a>API Management örneği oluşturma
Aşağıdaki API Management toomanage kullanma hello AzureML web hizmetiniz adımlardır. İlk olarak bir hizmet örneği oluşturun. İçinde toohello oturum [Klasik Portal](https://manage.windowsazure.com/) tıklatıp **yeni** > **uygulama hizmetleri** > **API Management**  >  **Oluşturma**.

![Örnek Oluştur](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

Benzersiz bir belirtin **URL**. Bu kılavuzu kullanır **demoazureml** – toochoose bir şey farklı gerekir. İstenen hello seçin **abonelik** ve **bölge** hizmet Örneğiniz için. Seçimlerinizi yaptıktan sonra hello İleri düğmesine tıklayın.

![oluşturma-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

Hello için bir değer belirtin **kuruluş adı**. Bu kılavuzu kullanır **demoazureml** – toochoose bir şey farklı gerekir. E-posta adresinizi hello **yönetici e-posta** alan. Bu e-posta adresi hello API Management sisteminden gelen bildirimler için kullanılır.

![oluşturma-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

Merhaba onay kutusunu toocreate hizmet örneğiniz'ı tıklatın. *Oluşturulan yeni bir hizmet toobe toothirty dakika kaplar*.

## <a name="create-hello-api"></a>Merhaba API'si oluşturma
Merhaba hizmet örneği oluşturulduktan sonra sonraki adıma hello toocreate hello API'dır. Bir API, istemci uygulamasından çağrılabilen işlemler grubundan oluşur. API işlemleri yönlendirilirken tooexisting web hizmetleridir. Bu kılavuz API'leri AzureML RRS ve BES web Hizmetleri varolan bu proxy toohello oluşturur.

API oluşturulur ve hello Klasik Azure portalı erişilen hello API yayımcı portalında yapılandırılır. Hizmet örneği tooreach hello yayımcı portalı, seçin.

![Select hizmet örneği](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

Tıklatın **Yönet** API Management hizmetiniz için Klasik Azure portalı hello içinde.

![yönetme hizmeti](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

Tıklatın **API'leri** hello gelen **API Management** sol hello ve ardından menüsünde **API Ekle**.

![API yönetimi menüsü](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

Tür **AzureML Demo API** hello olarak **Web API adı**. Tür **https://ussouthcentral.services.azureml.net** hello olarak **Web hizmeti URL'si**. Tür **azureml demo** hello olarak **Web API'si URL soneki**. Denetleme **HTTPS** hello olarak **Web API'si URL** düzeni. Seçin **Starter** olarak **ürünleri**. Tamamlandığında tıklatarak **kaydetmek** toocreate hello API.

![Yeni-API Ekle](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a>Merhaba işlemleri ekleme
Tıklatın **ekleme işlemi** tooadd operations toothis API.

![ekleme işlemi](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

Merhaba **yeni işlem** penceresinde görüntülenir ve hello **imza** sekmesi varsayılan olarak seçilir.

## <a name="add-rrs-operation"></a>RRS işlemi ekleyin
İlk hello AzureML RRS hizmeti için bir işlem oluşturun. Seçin **POST** hello olarak **HTTP fiili**. Türü **/workspaces/ {çalışma} /services/ {hizmeti} / execute? api-version {apiversion} = & Ayrıntıları {ayrıntıları} =** hello olarak **URL şablon**. Tür **RRS yürütme** hello olarak **görünen adı**.

![rrs-işlemi-imza ekle](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

Tıklatın **yanıtları** > **ekleme** hello seçin ve sol üzerinde **200 Tamam**. Tıklatın **kaydetmek** toosave bu işlemi.

![Add-rrs işlemi-yanıt](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a>BES işlemleri ekleme
Ekran görüntüleri için dahil olmayan hello RR işlemi eklemek için çok benzer toothose oldukları gibi BES işlemleri hello.

### <a name="submit-but-not-start-a-batch-execution-job"></a>Bir toplu iş yürütme iş gönderme (ancak başlatılmamasına)
Tıklatın **ekleme işlemi** tooadd hello AzureML BES işlemi toohello API. Seçin **POST** hello için **HTTP fiili**. Türü **/workspaces/ {çalışma} /services/ {hizmeti} / işleri? api-version = {apiversion}** hello için **URL şablon**. Tür **BES gönderme** hello için **görünen adı**. Tıklatın **yanıtları** > **ekleme** hello seçin ve sol üzerinde **200 Tamam**. Tıklatın **kaydetmek** toosave bu işlemi.

### <a name="start-a-batch-execution-job"></a>Bir toplu iş yürütme işi Başlat
Tıklatın **ekleme işlemi** tooadd hello AzureML BES işlemi toohello API. Seçin **POST** hello için **HTTP fiili**. Türü **/workspaces/ {çalışma} /services/ {hizmeti} /jobs/ {JobId} / start? api-version = {apiversion}** hello için **URL şablon**. Tür **BES Başlat** hello için **görünen adı**. Tıklatın **yanıtları** > **ekleme** hello seçin ve sol üzerinde **200 Tamam**. Tıklatın **kaydetmek** toosave bu işlemi.

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a>Merhaba durum ya da bir toplu iş yürütme iş sonucu alın
Tıklatın **ekleme işlemi** tooadd hello AzureML BES işlemi toohello API. Seçin **almak** hello için **HTTP fiili**. Türü **/workspaces/ {çalışma} /services/ {hizmeti} /jobs/ {JobId}? api-version = {apiversion}** hello için **URL şablon**. Tür **BES durum** hello için **görünen adı**. Tıklatın **yanıtları** > **ekleme** hello seçin ve sol üzerinde **200 Tamam**. Tıklatın **kaydetmek** toosave bu işlemi.

### <a name="delete-a-batch-execution-job"></a>Bir toplu iş yürütme iş Sil
Tıklatın **ekleme işlemi** tooadd hello AzureML BES işlemi toohello API. Seçin **silmek** hello için **HTTP fiili**. Türü **/workspaces/ {çalışma} /services/ {hizmeti} /jobs/ {JobId}? api-version = {apiversion}** hello için **URL şablon**. Tür **BES silmek** hello için **görünen adı**. Tıklatın **yanıtları** > **ekleme** hello seçin ve sol üzerinde **200 Tamam**. Tıklatın **kaydetmek** toosave bu işlemi.

## <a name="call-an-operation-from-hello-developer-portal"></a>Merhaba Geliştirici Portalı ' bir işlem çağırma
İşlemler uygun şekilde tooview sağlayan doğrudan hello Geliştirici portalından çağrılabilir ve bir API'nin işlemlerini hello test edin. Bu kılavuzu adımında, çağıracaktır hello **RRS yürütme** toohello eklendi yöntemi **AzureML Demo API**. Tıklatın **Geliştirici Portalı** hello hello menüden top hello Klasik Portal sağındaki.

![Geliştirici Portalı](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

Tıklatın **API'leri** hello üst menüsünden ve ardından **AzureML Demo API** toosee hello işlemleri kullanılabilir.

![demoazureml API](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

Seçin **RRS yürütme** hello işlemi için. Tıklatın **deneyin**.

![try-BT](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

İstek parametreleri için yazın, **çalışma**, **hizmet**, **2.0** hello için **apiversion**, ve **true**hello için **ayrıntıları**. Bulabilirsiniz, **çalışma** ve **hizmet** hello AzureML web hizmeti panosunda (bkz **Test hello web hizmeti** ek A içinde).

İstek üstbilgilerini için tıklatın **Ekle üstbilgi** ve türü **Content-Type** ve **uygulama/json**, ardından **Ekle üstbilgi** ve türü **yetkilendirme** ve **taşıyıcı <YOUR AZUREML SERVICE API-KEY>** . Bulabilirsiniz, **API anahtarı** hello AzureML web hizmeti panosunda (bkz **Test hello web hizmeti** ek A içinde).

Tür **{"Girişler": {"input1": {"ColumnNames": "Değerlerini" ["Col2"]: [["Bu bir iyi günüdür"]]}}, "GlobalParameters": {}}** hello istek gövdesi için.

![azureml demo API](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

Tıklatın **Gönder**.

![Gönder](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

Bir işlem çağrıldıktan sonra hello Geliştirici Portalı hello görüntüler **istenen URL** hello arka uç hizmetinden hello **yanıt durumu**, hello **yanıt üstbilgilerini**, ve tüm **yanıt içeriği**.

![yanıt durumu](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a>Ek A - web hizmeti oluşturma ve basit bir AzureML test etme
### <a name="creating-hello-experiment"></a>Merhaba deneme oluşturma
Basit bir AzureML deneme oluşturma ve bir web hizmeti olarak dağıtma hello adımları aşağıda verilmiştir. Web hizmeti alır, rastgele metin sütunu giriş olarak hello ve bir tamsayı olarak temsil özellik kümesi döndürür. Örneğin:

| Metin | Karma metin |
| --- | --- |
| Bu iyi bir günüdür |1 1 2 2 0 2 0 1 |

İlk olarak, tercih ettiğiniz bir tarayıcı kullanarak gidin için: [https://studio.azureml.net/](https://studio.azureml.net/) ve, kimlik bilgileri toolog girin. Ardından, yeni bir boş deneme oluşturun.

![Arama deneme şablonları](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

Çok yeniden adlandırma**SimpleFeatureHashingExperiment**. Genişletme **kaydedilen veri kümeleri** ve sürükleyin **Kitap incelemeleri Amazon gelen** denemenizi üzerine.

![Basit-özellik-karma-deneme](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

Genişletme **veri dönüştürme** ve **işleme** ve sürükleyin **Select Columns in Dataset sütun** denemenizi üzerine. Bağlantı **Kitap incelemeleri Amazon gelen** çok**Select Columns in Dataset sütun**.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

Tıklatın **Select Columns in Dataset sütun** ve ardından **başlatma Sütun seçiciyi** seçip **Col2**. Bu değişiklikler Hello onay işareti tooapply tıklayın.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

Genişletme **metin analizi** ve sürükleyin **özellik karma** hello deneme üzerine. Bağlantı **Select Columns in Dataset sütun** çok**özellik karma**.

![Connect-proje-sütunlar](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

Tür **3** hello için **bitsize karma**. Bu 8 (23) oluşturacak sütun.

![karma bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

Bu noktada, tooclick isteyebilirsiniz **çalıştırmak** tootest hello deneme.

![çalıştırma](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a>Web hizmeti oluşturma
Şimdi bir web hizmeti oluşturun. Genişletme **Web hizmeti** ve sürükleyin **giriş** denemenizi üzerine. Bağlantı **giriş** çok**özellik karma**. Ayrıca sürükleyin **çıkış** denemenizi üzerine. Bağlantı **çıkış** çok**özellik karma**.

![Çıktı-için-özellik-karma](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

Tıklatın **web hizmeti yayımlama**.

![Yayımlama-web hizmeti](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

Tıklatın **Evet** toopublish hello deneme.

![Yayımlama Evet](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a>Test hello web hizmeti
AzureML web hizmeti RSS (istek/yanıt hizmeti) ve BES (toplu yürütme hizmeti) uç noktaları oluşur. RSS için zaman uyumlu yürütme ' dir. BES için zaman uyumsuz iş yürütme ' dir. web hizmeti hello örnek Python kaynağı ile aşağıdaki tootest ihtiyacınız olabilecek toodownload ve yükleme hello Azure SDK'sı için Python (bkz: [nasıl tooinstall Python](../python-how-to-install.md)).

Merhaba de gerekir **çalışma**, **hizmet**, ve **apı_key** denemenizi hello örnek kaynağı için. Ya da tıklatarak hello çalışma ve hizmet bulabilirsiniz **istek/yanıt** veya **toplu iş yürütme** hello web hizmeti panosunda denemeniz için.

![Bul çalışma-ve-hizmet](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

Merhaba bulabilirsiniz **apı_key** denemenizi hello web hizmeti panosunda tıklatarak.

![Bul API anahtarı](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a>Test RRS uç noktası
##### <a name="test-button"></a>Test düğmesi
Tooclick bir kolay bir yolu tootest hello RR uç noktadır **Test** hello web hizmeti panosundaki.

![test etme](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

Tür **bu iyi bir günüdür** için **col2**. Merhaba onay işaretine tıklayın.

![veri girme](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

Şöyle görürsünüz

![örnek çıktı](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a>Örnek kod
Başka bir şekilde tootest, RRS istemci kodunuzdan ' dir. Tıklatırsanız **istek/yanıt** hello Pano ve kaydırma toohello altta, örnek kod C#, Python ve r görürsünüz Merhaba sözdizimi hello RRS isteği hello isteğin URI, üst bilgiler ve gövde dahil olmak üzere, ayrıca görürsünüz.

Bu kılavuz, çalışan bir Python örneği gösterir. Toomodify gerekir hello ile **çalışma**, **hizmet**, ve **apı_key** denemenizi biri.

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a>Test BES uç noktası
Tıklatın **toplu yürütme** altta hello Pano ve kaydırma toohello. C#, Python ve r için örnek kod görürsünüz Ayrıca, BES istekleri toosubmit bir işi Merhaba, bir işi başlatmak, hello durumu veya bir iş sonuçlarını almak ve bir işi silmek hello sözdizimi görürsünüz.

Bu kılavuz, çalışan bir Python örneği gösterir. Toomodify ihtiyacınız hello ile **çalışma**, **hizmet**, ve **apı_key** denemenizi biri. Ayrıca, toomodify hello ihtiyacınız **depolama hesabı adı**, **depolama hesabı anahtarı**, ve **depolama kapsayıcısı adı**. Son olarak, toomodify hello hello konumunu gerekir **giriş dosyası** ve hello hello konumunu **çıktı dosyası**.

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
