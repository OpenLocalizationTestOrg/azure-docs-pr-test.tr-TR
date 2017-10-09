---
title: "Azure Cosmos DB için aaaPython Flask web uygulaması Öğreticisi | Microsoft Docs"
description: "Azure Cosmos DB toostore ve erişim verilerini Azure üzerinde barındırılan bir Python Flask web uygulamasından kullanma konulu veritabanı öğreticisini inceleyin. Uygulama geliştirme çözümleri bulun."
keywords: "Uygulama geliştirme, python flask, python web uygulaması, python web geliştirme"
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a>Azure Cosmos DB kullanarak bir Python Flask web uygulaması derleme
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Bu öğretici nasıl toouse Azure Cosmos DB toostore ve erişim verilerini bir Python web uygulaması Azure üzerinde barındırılan ve Python ve Azure Web sitelerini kullanma konusunda biraz deneyim sahibi olduğunuzu varsayar gösterir.

Bu veritabanı öğreticisi şunlara değinir:

1. Oluşturma ve Cosmos DB hesap sağlama.
2. Bir Python Flask uygulaması oluşturuluyor.
3. Cosmos DB web uygulamanızı kullanarak tooand bağlanıyor.
4. Merhaba web uygulama tooAzure dağıtma.

Bu öğreticiyi izleyerek bir yoklama için toovote sağlayan basit bir oylama uygulaması oluşturacaksınız.

![Bu veritabanı Öğreticisi tarafından oluşturulan hello oylama uygulamasının ekran görüntüsü](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a>Veritabanı öğreticisi önkoşulları
Bu makaledeki Hello yönergeleri izlemeden önce hello aşağıdaki yüklü olduğundan emin olmanız gerekir:

* Etkin bir Azure hesabı. Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).
 
    OR 

    Merhaba yerel yüklemesi [Azure Cosmos DB öykünücüsü](local-emulator.md).
* [Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).  
* [Visual Studio için Python Araçları](https://github.com/Microsoft/PTVS/).  
* [Python 2.7 için Microsoft Azure SDK](https://azure.microsoft.com/downloads/). 
* [Python 2.7.13](https://www.python.org/downloads/windows/). 

> [!IMPORTANT]
> Python 2.7 için hello ilk kez yüklüyorsanız hello Python 2.7.13 özelleştirme ekranında belirlediğinizden emin olun **Python.exe'yi tooPath eklemek**.
> 
> ![Tooselect Ekle Python.exe'yi tooPath ihtiyaç duyacağınız hello Python 2.7.11'i özelleştirme ekranının ekran görüntüsü](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* [Python 2.7 için Microsoft Visual C++ derleyicisi](https://www.microsoft.com/en-us/download/details.aspx?id=44266).

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a>1. Adım: Azure Cosmos DB veritabanı hesabı oluşturma
İlk olarak bir Cosmos DB hesabı oluşturalım. Zaten bir hesabınız yok veya kullanıyorsanız bu öğretici için Azure Cosmos DB öykünücüsü hello kullanıyorsanız, çok atlayabilirsiniz[2. adım: yeni bir Python Flask web uygulaması oluşturma](#step-2-create-a-new-python-flask-web-application).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
Biz şimdi toocreate hello yeni bir Python Flask web uygulamasından nasıl plan size yol gösterecek.

## <a name="step-2-create-a-new-python-flask-web-application"></a>2. Adım: Yeni bir Python Flask web uygulaması oluşturma
1. Visual Studio'da, hello **dosya** menüsünde çok noktası**yeni**ve ardından **proje**.
   
    Merhaba **yeni proje** iletişim kutusu görüntülenir.
2. Merhaba sol bölmesinde **şablonları** ve ardından **Python**ve ardından **Web**. 
3. Seçin **Flask Web projesi** hello bölmeyi ardından hello **adı** kutusuna **öğretici**ve ardından **Tamam**. Python paket adlarının hello açıklandığı gibi tamamen küçük harfli olması gerektiğini unutmayın [Python kodu için Stil Kılavuzu](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).
   
    Bu yeni tooPython için Flask, onu python'da web uygulamalarını daha hızlı oluşturmanıza yardımcı olan bir web uygulaması geliştirme altyapısıdır.
   
    ![Visual Studio'da sol, Python Flask Web projesi hello Orta ve hello adı öğretici hello adı kutusunda seçili hello vurgulanmış Python ile Merhaba yeni proje penceresinin ekran görüntüsü](./media/documentdb-python-application/image9.png)
4. Merhaba, **Visual Studio için Python Araçları** penceresinde tıklatın **sanal bir ortama yükleme**. 
   
    ![Merhaba veritabanı Öğreticisi - Visual Studio penceresi için Python Araçları'nın ekran görüntüsü](./media/documentdb-python-application/python-install-virtual-environment.png)
5. Merhaba, **sanal ortam Ekle** penceresinde hello Varsayılanları kabul edin ve PyDocumentDB şu anda Python desteklemediğinden Python 2.7 hello temel ortam olarak kullanabilirsiniz 3.x ve ardından **oluşturma**. Bu gerekli hello Python sanal ortamı projeniz için ayarlar.
   
    ![Merhaba veritabanı Öğreticisi - Visual Studio penceresi için Python Araçları'nın ekran görüntüsü](./media/documentdb-python-application/image10_A.png)
   
    Merhaba çıktı penceresinde görüntüler `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` hello ortam başarıyla yüklü olduğunda.

## <a name="step-3-modify-hello-python-flask-web-application"></a>3. adım: hello Python Flask web uygulamasını değiştirme
### <a name="add-hello-python-flask-packages-tooyour-project"></a>Merhaba Python Flask paketlerini tooyour proje ekleyin
Projeniz kurulduktan sonra pydocumentdb ve DocumentDB için hello Python paket dahil olmak üzere tooadd hello gerekli Flask paketlerini tooyour proje, gerekir.

1. Çözüm Gezgini'nde adlı hello dosyasını açın **requirements.txt** ve hello içeriği hello şununla değiştirin:
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. Merhaba Kaydet **requirements.txt** dosya. 
3. Çözüm Gezgini'nde **env**'e sağ tıklayın ve **requirements.txt'ten yükle**'ye tıklayın.
   
    ![Merhaba listesinde vurgulanan requirements.txt yükleme işlemine seçildiği gösteren env (Python 2.7) ekran görüntüsü](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    Başarılı yüklemeden sonra hello çıkış penceresi hello şunları görüntüler:
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > Nadir durumlarda hello çıktı penceresinde bir hata görebilirsiniz. Bu durumda, hello hata ilgili toocleanup olup olmadığını denetleyin. Bazen hello temizleme başarısız olur, ancak hello yükleme hala başarılı olacaktır (yukarı hello çıktı penceresi tooverify bu kaydırma). Yüklemenizi denetleyebilirsiniz [doğrulama hello sanal ortam](#verify-the-virtual-environment). Merhaba yüklemesi başarısız oldu, ancak hello doğrulama başarılı olur, Tamam toocontinue olur.
   > 
   > 

### <a name="verify-hello-virtual-environment"></a>Merhaba sanal ortamı doğrulama
Her şeyin doğru şekilde yüklendiğinden emin olmamız gerekir.

1. Tuşlarına basarak Hello çözümü derleme **Ctrl**+**Shift**+**B**.
2. Merhaba derleme başarılı olduktan sonra basarak hello Web sitesini başlatın **F5**. Bu hello Flask geliştirme sunucusu başlatılmış ve web tarayıcınız başlatılır. Sayfa aşağıdaki hello görmeniz gerekir.
   
    ![Merhaba boş Python Flask web geliştirme projesi bir tarayıcıda görüntülenen](./media/documentdb-python-application/image12.png)
3. Basarak Hello Web sitesinin hata ayıklamasını durdurun **Shift**+**F5** Visual Studio.

### <a name="create-database-collection-and-document-definitions"></a>Veritabanı, koleksiyon ve belge tanımları oluşturma
Şimdi yeni dosyalar ekleyip diğer dosyaları güncelleştirerek oylama uygulamanızı oluşturalım.

1. Çözüm Gezgini'nde hello sağ **öğretici** proje, tıklatın **Ekle**ve ardından **yeni öğe**. Seçin **boş Python dosyası** ve ad hello dosya **forms.py**.  
2. Aşağıdaki kod toohello forms.py dosyasına hello ekleyin ve hello dosyasını kaydedin.

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a>Gerekli hello içeri aktarmalar tooviews.py Ekle
1. Çözüm Gezgini'nde hello genişletin **öğretici** klasörü ve açık hello **views.py** dosya. 
2. İçeri aktarma deyimlerini toohello hello üstündeki aşağıdaki hello eklemek **views.py** dosya ardından hello dosyasını kaydedin. Bunlar Cosmos veritabanı pythonsdk'sını alın ve Flask paketlerini hello.
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a>Veritabanı, koleksiyon ve belge oluşturma
* Hala **views.py**, kod toohello hello dosyasının sonuna aşağıdaki hello ekleyin. Bu alan hello form tarafından kullanılan hello veritabanı oluşturmayı dikkat edin. Merhaba var olan kodda silmeyin **views.py**. Yalnızca bu toohello son ekleyin.

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a>Veritabanı, koleksiyon ve belge okuma ve form gönderme
* Hala **views.py**, kod toohello hello dosyasının sonuna aşağıdaki hello ekleyin. Bu alan hello veritabanı, koleksiyon ve belge okuma hello formu, gerçekleşmiş olur. Merhaba var olan kodda silmeyin **views.py**. Yalnızca bu toohello son ekleyin.

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a>Merhaba HTML dosyaları oluşturma
1. Çözüm Gezgini'nde, hello **öğretici** klasörü, sağ tıklatın hello **şablonları** klasörü, tıklatın **Ekle**ve ardından **yeni öğe**. 
2. Seçin **HTML sayfası**ve ardından hello ad kutusuna **create.html**. 
3. Adım 1 ve 2 toocreate iki ek HTML dosyası tekrarlayın: results.html ve vote.html.
4. Kod çok aşağıdaki hello eklemek**create.html** hello içinde `<body>` öğesi. Yeni bir veritabanı, koleksiyon ve belge oluşturduğumuzu bildiren bir ileti görüntülenir.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. Kod çok aşağıdaki hello eklemek**results.html** hello içinde `<body`> öğesi. Merhaba yoklama hello sonuçlarını görüntüler.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. Kod çok aşağıdaki hello eklemek**vote.html** hello içinde `<body`> öğesi. Merhaba yoklamayı görüntüler ve hello oyları kabul eder. Merhaba oy kaydetmede hello Denetim burada biz hello oy tanıyacağımız ve hello belge buna uygun olarak eklenecek tooviews.py geçirilir.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. Merhaba, **şablonları** klasörü Değiştir Merhaba içeriğine **index.html** hello aşağıdaki ile. Bu, giriş sayfasında uygulamanız için hello görür.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a>Bir yapılandırma dosyası ekleme ve değiştirme hello \_ \_init\_\_.py
1. Çözüm Gezgini'nde hello sağ **öğretici** projesi,'ı tıklatın **Ekle**, tıklatın **yeni öğe**seçin **boş Python dosyası**ve ardından ad hello dosyası **documentdb**. Bu yapılandırma dosyası, Flask'taki formlar için gereklidir. Tooprovide gizli bir anahtar da kullanabilirsiniz. Ancak bu anahtar bu öğretici için gerekli değildir.
2. Merhaba aşağıdakileri ekleyin kod tooconfig.py tooalter hello değerlerini gerekir **DOCUMENTDB\_KONAK** ve **DOCUMENTDB\_anahtar** hello sonraki adımda.
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. Merhaba, [Azure portal](https://portal.azure.com/), toohello gidin **anahtarları** dikey **Gözat**, **Azure Cosmos DB hesapları**, hello adına çift tıklayın Merhaba, toouse hesap ve hello ardından **anahtarları** hello düğmesini **Essentials** alanı. Merhaba, **anahtarları** dikey penceresinde, kopyalama hello **URI** değer ve hello yapıştırma **documentdb** hello hello değeri olarak dosya **DOCUMENTDB\_ana bilgisayar**  özelliği. 
4. Hello Azure portalında, hello edilene **anahtarları** dikey penceresinde hello kopyalama hello değeri **birincil anahtar** veya hello **ikincil anahtar**ve hello yapıştırma **documentdb**  hello hello değeri olarak dosya **DOCUMENTDB\_anahtar** özelliği.
5. Merhaba,  **\_ \_init\_\_.py** dosya, aşağıdaki satırı hello ekleyin. 
   
        app.config.from_object('config')
   
    Böylece hello dosyanın Merhaba içeriğine olur:
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. Tüm hello dosyaları ekledikten sonra Çözüm Gezgini aşağıdaki gibi görünmelidir:
   
    ![Merhaba Visual Studio Çözüm Gezgini penceresinin ekran görüntüsü](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a>4. Adım: Web uygulamanızı yerel olarak çalıştırma
1. Tuşlarına basarak Hello çözümü derleme **Ctrl**+**Shift**+**B**.
2. Merhaba derleme başarılı olduktan sonra basarak hello Web sitesini başlatın **F5**. Ekranda hello şunları görmeniz gerekir.
   
    ![Ekran Merhaba Python + Azure Cosmos DB oylama bir web tarayıcısında görüntülenen uygulama görüntüsü](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. Tıklatın **oylama veritabanını oluştur/Temizle hello** toogenerate hello veritabanı.
   
    ![Ekran görüntüsü oluşturma sayfası'hello web uygulamasının – geliştirme ayrıntıları hello](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. Ardından **Oy Ver**'e tıklayın ve seçiminizi belirleyin.
   
    ![Bir oylama sorusu sorulmuş web uygulamasıyla hello ekran görüntüsü](./media/documentdb-python-application/cosmos-db-vote.png)
5. Verdiğiniz her oy için bunu hello uygun sayaç artırılır.
   
    ![Hello sonuçları gösterilen hello oy sayfasının ekran görüntüsü](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. Shift + F5'e basarak Hello proje hata ayıklamayı durdurun.

## <a name="step-5-deploy-hello-web-application-tooazure"></a>5. adım: hello web uygulama tooAzure dağıtma
Merhaba tam uygulaması düzgün çalıştığından Cosmos DB karşı sahip olduğunuza göre bu tooAzure toodeploy yapacağız.

1. Çözüm Gezgini'nde hello projeye sağ tıklayın (etmediğinizden emin olun hala yerel olarak çalışan) seçip **Yayımla**.  
   
     ![Çözüm Gezgini'nde hello Yayımla seçeneği vurgulanmış seçili hello Öğreticisi ekran görüntüsü](./media/documentdb-python-application/image20.png)
2. Merhaba, **Yayımla** iletişim kutusunda **Microsoft Azure App Service**seçin **Yeni Oluştur**ve ardından **Yayımla**.
   
    ![Microsoft Azure App Service vurgulanmış hello Web'de Yayımla penceresinin ekran görüntüsü](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. Merhaba, **App Service Oluştur** iletişim kutusunda, web uygulamanız ile birlikte hello adını girin, **abonelik**, **kaynak grubu**, ve **App Service planı** , ardından **oluşturma**.
   
    ![Merhaba Microsoft Azure Web Apps penceresi penceresinin ekran görüntüsü](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. Birkaç saniye içinde Visual Studio uygulama hizmetiniz yayımlamayı bitirecek ve Azure'da çalışan, handiwork görebileceğiniz bir tarayıcıyı başlatacak!

    ![Merhaba Microsoft Azure Web Apps penceresi penceresinin ekran görüntüsü](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a>Sorun giderme
Bilgisayarınızda çalıştırın hello ilk Python uygulaması buysa, o hello aşağıdakilerden emin olun klasörlerin (veya hello eşdeğer yükleme konumlarının) yol değişkeninize bulunmaktadır:

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

Oy sayfanızda bir hata alırsanız ve projenize bir şey dışında adlı **öğretici**, olduğundan emin olun  **\_ \_init\_\_.py** başvuruları hello hello satır doğru proje adına: `import tutorial.view`.

## <a name="next-steps"></a>Sonraki adımlar
Tebrikler! Yalnızca Cosmos DB kullanarak ilk Python web uygulamanızı tamamladınız ve tooAzure yayımlanan.

Geri bildirimlerinizi temel alarak bu konu başlığını sıklıkla güncelleştirip iyileştiriyoruz.  Bir kez hello öğretici, lütfen oylama düğmeleri hello en üstündeki ve bu sayfanın hello tamamladıktan ve yapılan toosee istediğiniz hangi iyileştirmeler hakkında geri bildirim emin tooinclude olabilir. Bize istiyorsanız toocontact doğrudan düşündüğünüz e-posta adresi serbest tooinclude yorumlarınızı içinde.

tooadd ek işlevler tooyour web uygulaması, gözden geçirme hello API'leri hello kullanılabilir [Azure Cosmos DB Python SDK'sı](documentdb-sdk-python.md).

Azure, Visual Studio ve Python hakkında daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](https://azure.microsoft.com/develop/python/). 

Ek Python Flask öğreticileri için bkz: [hello büyük Flask Öğreticisi, bölümü I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world). 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
