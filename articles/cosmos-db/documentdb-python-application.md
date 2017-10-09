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
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="6b386-105">Azure Cosmos DB kullanarak bir Python Flask web uygulaması derleme</span><span class="sxs-lookup"><span data-stu-id="6b386-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b386-106">.NET</span><span class="sxs-lookup"><span data-stu-id="6b386-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="6b386-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="6b386-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="6b386-108">Java</span><span class="sxs-lookup"><span data-stu-id="6b386-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="6b386-109">Python</span><span class="sxs-lookup"><span data-stu-id="6b386-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="6b386-110">Bu öğretici nasıl toouse Azure Cosmos DB toostore ve erişim verilerini bir Python web uygulaması Azure üzerinde barındırılan ve Python ve Azure Web sitelerini kullanma konusunda biraz deneyim sahibi olduğunuzu varsayar gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b386-110">This tutorial shows you how toouse Azure Cosmos DB toostore and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="6b386-111">Bu veritabanı öğreticisi şunlara değinir:</span><span class="sxs-lookup"><span data-stu-id="6b386-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="6b386-112">Oluşturma ve Cosmos DB hesap sağlama.</span><span class="sxs-lookup"><span data-stu-id="6b386-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="6b386-113">Bir Python Flask uygulaması oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="6b386-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="6b386-114">Cosmos DB web uygulamanızı kullanarak tooand bağlanıyor.</span><span class="sxs-lookup"><span data-stu-id="6b386-114">Connecting tooand using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="6b386-115">Merhaba web uygulama tooAzure dağıtma.</span><span class="sxs-lookup"><span data-stu-id="6b386-115">Deploying hello web application tooAzure.</span></span>

<span data-ttu-id="6b386-116">Bu öğreticiyi izleyerek bir yoklama için toovote sağlayan basit bir oylama uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="6b386-116">By following this tutorial, you will build a simple voting application that allows you toovote for a poll.</span></span>

![Bu veritabanı Öğreticisi tarafından oluşturulan hello oylama uygulamasının ekran görüntüsü](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="6b386-118">Veritabanı öğreticisi önkoşulları</span><span class="sxs-lookup"><span data-stu-id="6b386-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="6b386-119">Bu makaledeki Hello yönergeleri izlemeden önce hello aşağıdaki yüklü olduğundan emin olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6b386-119">Before following hello instructions in this article, you should ensure that you have hello following installed:</span></span>

* <span data-ttu-id="6b386-120">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="6b386-120">An active Azure account.</span></span> <span data-ttu-id="6b386-121">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b386-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6b386-122">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b386-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="6b386-123">OR</span><span class="sxs-lookup"><span data-stu-id="6b386-123">OR</span></span> 

    <span data-ttu-id="6b386-124">Merhaba yerel yüklemesi [Azure Cosmos DB öykünücüsü](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="6b386-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="6b386-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="6b386-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="6b386-126">[Visual Studio için Python Araçları](https://github.com/Microsoft/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="6b386-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="6b386-127">[Python 2.7 için Microsoft Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6b386-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="6b386-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="6b386-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6b386-129">Python 2.7 için hello ilk kez yüklüyorsanız hello Python 2.7.13 özelleştirme ekranında belirlediğinizden emin olun **Python.exe'yi tooPath eklemek**.</span><span class="sxs-lookup"><span data-stu-id="6b386-129">If you are installing Python 2.7 for hello first time, ensure that in hello Customize Python 2.7.13 screen, you select **Add python.exe tooPath**.</span></span>
> 
> ![Tooselect Ekle Python.exe'yi tooPath ihtiyaç duyacağınız hello Python 2.7.11'i özelleştirme ekranının ekran görüntüsü](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="6b386-131">[Python 2.7 için Microsoft Visual C++ derleyicisi](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span><span class="sxs-lookup"><span data-stu-id="6b386-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="6b386-132">1. Adım: Azure Cosmos DB veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b386-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="6b386-133">İlk olarak bir Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="6b386-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="6b386-134">Zaten bir hesabınız yok veya kullanıyorsanız bu öğretici için Azure Cosmos DB öykünücüsü hello kullanıyorsanız, çok atlayabilirsiniz[2. adım: yeni bir Python Flask web uygulaması oluşturma](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="6b386-134">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="6b386-135">Biz şimdi toocreate hello yeni bir Python Flask web uygulamasından nasıl plan size yol gösterecek.</span><span class="sxs-lookup"><span data-stu-id="6b386-135">We will now walk through how toocreate a new Python Flask web application from hello ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="6b386-136">2. Adım: Yeni bir Python Flask web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b386-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="6b386-137">Visual Studio'da, hello **dosya** menüsünde çok noktası**yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="6b386-137">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="6b386-138">Merhaba **yeni proje** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6b386-138">hello **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="6b386-139">Merhaba sol bölmesinde **şablonları** ve ardından **Python**ve ardından **Web**.</span><span class="sxs-lookup"><span data-stu-id="6b386-139">In hello left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="6b386-140">Seçin **Flask Web projesi** hello bölmeyi ardından hello **adı** kutusuna **öğretici**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6b386-140">Select **Flask  Web Project** in hello center pane, then in hello **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="6b386-141">Python paket adlarının hello açıklandığı gibi tamamen küçük harfli olması gerektiğini unutmayın [Python kodu için Stil Kılavuzu](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="6b386-141">Remember that Python package names should be all lowercase, as described in hello [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="6b386-142">Bu yeni tooPython için Flask, onu python'da web uygulamalarını daha hızlı oluşturmanıza yardımcı olan bir web uygulaması geliştirme altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="6b386-142">For those new tooPython Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Visual Studio'da sol, Python Flask Web projesi hello Orta ve hello adı öğretici hello adı kutusunda seçili hello vurgulanmış Python ile Merhaba yeni proje penceresinin ekran görüntüsü](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="6b386-144">Merhaba, **Visual Studio için Python Araçları** penceresinde tıklatın **sanal bir ortama yükleme**.</span><span class="sxs-lookup"><span data-stu-id="6b386-144">In hello **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Merhaba veritabanı Öğreticisi - Visual Studio penceresi için Python Araçları'nın ekran görüntüsü](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="6b386-146">Merhaba, **sanal ortam Ekle** penceresinde hello Varsayılanları kabul edin ve PyDocumentDB şu anda Python desteklemediğinden Python 2.7 hello temel ortam olarak kullanabilirsiniz 3.x ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6b386-146">In hello **Add Virtual Environment** window, you can accept hello defaults and use Python 2.7 as hello base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="6b386-147">Bu gerekli hello Python sanal ortamı projeniz için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="6b386-147">This sets up hello required Python virtual environment for your project.</span></span>
   
    ![Merhaba veritabanı Öğreticisi - Visual Studio penceresi için Python Araçları'nın ekran görüntüsü](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="6b386-149">Merhaba çıktı penceresinde görüntüler `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` hello ortam başarıyla yüklü olduğunda.</span><span class="sxs-lookup"><span data-stu-id="6b386-149">hello output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when hello environment is successfully installed.</span></span>

## <a name="step-3-modify-hello-python-flask-web-application"></a><span data-ttu-id="6b386-150">3. adım: hello Python Flask web uygulamasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="6b386-150">Step 3: Modify hello Python Flask web application</span></span>
### <a name="add-hello-python-flask-packages-tooyour-project"></a><span data-ttu-id="6b386-151">Merhaba Python Flask paketlerini tooyour proje ekleyin</span><span class="sxs-lookup"><span data-stu-id="6b386-151">Add hello Python Flask packages tooyour project</span></span>
<span data-ttu-id="6b386-152">Projeniz kurulduktan sonra pydocumentdb ve DocumentDB için hello Python paket dahil olmak üzere tooadd hello gerekli Flask paketlerini tooyour proje, gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b386-152">After your project is set up, you'll need tooadd hello required Flask packages tooyour project, including pydocumentdb, hello Python package for DocumentDB.</span></span>

1. <span data-ttu-id="6b386-153">Çözüm Gezgini'nde adlı hello dosyasını açın **requirements.txt** ve hello içeriği hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6b386-153">In Solution Explorer, open hello file named **requirements.txt** and replace hello contents with hello following:</span></span>
   
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
2. <span data-ttu-id="6b386-154">Merhaba Kaydet **requirements.txt** dosya.</span><span class="sxs-lookup"><span data-stu-id="6b386-154">Save hello **requirements.txt** file.</span></span> 
3. <span data-ttu-id="6b386-155">Çözüm Gezgini'nde **env**'e sağ tıklayın ve **requirements.txt'ten yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b386-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Merhaba listesinde vurgulanan requirements.txt yükleme işlemine seçildiği gösteren env (Python 2.7) ekran görüntüsü](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="6b386-157">Başarılı yüklemeden sonra hello çıkış penceresi hello şunları görüntüler:</span><span class="sxs-lookup"><span data-stu-id="6b386-157">After successful installation, hello output window displays hello following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="6b386-158">Nadir durumlarda hello çıktı penceresinde bir hata görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b386-158">In rare cases, you might see a failure in hello output window.</span></span> <span data-ttu-id="6b386-159">Bu durumda, hello hata ilgili toocleanup olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="6b386-159">If this happens, check if hello error is related toocleanup.</span></span> <span data-ttu-id="6b386-160">Bazen hello temizleme başarısız olur, ancak hello yükleme hala başarılı olacaktır (yukarı hello çıktı penceresi tooverify bu kaydırma).</span><span class="sxs-lookup"><span data-stu-id="6b386-160">Sometimes hello cleanup fails, but hello installation will still be successful (scroll up in hello output window tooverify this).</span></span> <span data-ttu-id="6b386-161">Yüklemenizi denetleyebilirsiniz [doğrulama hello sanal ortam](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="6b386-161">You can check your installation by [Verifying hello virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="6b386-162">Merhaba yüklemesi başarısız oldu, ancak hello doğrulama başarılı olur, Tamam toocontinue olur.</span><span class="sxs-lookup"><span data-stu-id="6b386-162">If hello installation failed but hello verification is successful, it's OK toocontinue.</span></span>
   > 
   > 

### <a name="verify-hello-virtual-environment"></a><span data-ttu-id="6b386-163">Merhaba sanal ortamı doğrulama</span><span class="sxs-lookup"><span data-stu-id="6b386-163">Verify hello virtual environment</span></span>
<span data-ttu-id="6b386-164">Her şeyin doğru şekilde yüklendiğinden emin olmamız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b386-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="6b386-165">Tuşlarına basarak Hello çözümü derleme **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="6b386-165">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="6b386-166">Merhaba derleme başarılı olduktan sonra basarak hello Web sitesini başlatın **F5**.</span><span class="sxs-lookup"><span data-stu-id="6b386-166">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="6b386-167">Bu hello Flask geliştirme sunucusu başlatılmış ve web tarayıcınız başlatılır.</span><span class="sxs-lookup"><span data-stu-id="6b386-167">This launches hello Flask development server and starts your web browser.</span></span> <span data-ttu-id="6b386-168">Sayfa aşağıdaki hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b386-168">You should see hello following page.</span></span>
   
    ![Merhaba boş Python Flask web geliştirme projesi bir tarayıcıda görüntülenen](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="6b386-170">Basarak Hello Web sitesinin hata ayıklamasını durdurun **Shift**+**F5** Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b386-170">Stop debugging hello website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="6b386-171">Veritabanı, koleksiyon ve belge tanımları oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b386-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="6b386-172">Şimdi yeni dosyalar ekleyip diğer dosyaları güncelleştirerek oylama uygulamanızı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="6b386-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="6b386-173">Çözüm Gezgini'nde hello sağ **öğretici** proje, tıklatın **Ekle**ve ardından **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="6b386-173">In Solution Explorer, right-click hello **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="6b386-174">Seçin **boş Python dosyası** ve ad hello dosya **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="6b386-174">Select **Empty Python File** and name hello file **forms.py**.</span></span>  
2. <span data-ttu-id="6b386-175">Aşağıdaki kod toohello forms.py dosyasına hello ekleyin ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6b386-175">Add hello following code toohello forms.py file, and then save hello file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a><span data-ttu-id="6b386-176">Gerekli hello içeri aktarmalar tooviews.py Ekle</span><span class="sxs-lookup"><span data-stu-id="6b386-176">Add hello required imports tooviews.py</span></span>
1. <span data-ttu-id="6b386-177">Çözüm Gezgini'nde hello genişletin **öğretici** klasörü ve açık hello **views.py** dosya.</span><span class="sxs-lookup"><span data-stu-id="6b386-177">In Solution Explorer, expand hello **tutorial** folder, and open hello **views.py** file.</span></span> 
2. <span data-ttu-id="6b386-178">İçeri aktarma deyimlerini toohello hello üstündeki aşağıdaki hello eklemek **views.py** dosya ardından hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6b386-178">Add hello following import statements toohello top of hello **views.py** file, then save hello file.</span></span> <span data-ttu-id="6b386-179">Bunlar Cosmos veritabanı pythonsdk'sını alın ve Flask paketlerini hello.</span><span class="sxs-lookup"><span data-stu-id="6b386-179">These import Cosmos DB's PythonSDK and hello Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="6b386-180">Veritabanı, koleksiyon ve belge oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b386-180">Create database, collection, and document</span></span>
* <span data-ttu-id="6b386-181">Hala **views.py**, kod toohello hello dosyasının sonuna aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6b386-181">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="6b386-182">Bu alan hello form tarafından kullanılan hello veritabanı oluşturmayı dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6b386-182">This takes care of creating hello database used by hello form.</span></span> <span data-ttu-id="6b386-183">Merhaba var olan kodda silmeyin **views.py**.</span><span class="sxs-lookup"><span data-stu-id="6b386-183">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="6b386-184">Yalnızca bu toohello son ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6b386-184">Simply append this toohello end.</span></span>

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


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="6b386-185">Veritabanı, koleksiyon ve belge okuma ve form gönderme</span><span class="sxs-lookup"><span data-stu-id="6b386-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="6b386-186">Hala **views.py**, kod toohello hello dosyasının sonuna aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6b386-186">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="6b386-187">Bu alan hello veritabanı, koleksiyon ve belge okuma hello formu, gerçekleşmiş olur.</span><span class="sxs-lookup"><span data-stu-id="6b386-187">This takes care of setting up hello form, reading hello database, collection, and document.</span></span> <span data-ttu-id="6b386-188">Merhaba var olan kodda silmeyin **views.py**.</span><span class="sxs-lookup"><span data-stu-id="6b386-188">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="6b386-189">Yalnızca bu toohello son ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6b386-189">Simply append this toohello end.</span></span>

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


### <a name="create-hello-html-files"></a><span data-ttu-id="6b386-190">Merhaba HTML dosyaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b386-190">Create hello HTML files</span></span>
1. <span data-ttu-id="6b386-191">Çözüm Gezgini'nde, hello **öğretici** klasörü, sağ tıklatın hello **şablonları** klasörü, tıklatın **Ekle**ve ardından **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="6b386-191">In Solution Explorer, in hello **tutorial** folder, right click hello **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="6b386-192">Seçin **HTML sayfası**ve ardından hello ad kutusuna **create.html**.</span><span class="sxs-lookup"><span data-stu-id="6b386-192">Select **HTML Page**, and then in hello name box type **create.html**.</span></span> 
3. <span data-ttu-id="6b386-193">Adım 1 ve 2 toocreate iki ek HTML dosyası tekrarlayın: results.html ve vote.html.</span><span class="sxs-lookup"><span data-stu-id="6b386-193">Repeat steps 1 and 2 toocreate two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="6b386-194">Kod çok aşağıdaki hello eklemek**create.html** hello içinde `<body>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="6b386-194">Add hello following code too**create.html** in hello `<body>` element.</span></span> <span data-ttu-id="6b386-195">Yeni bir veritabanı, koleksiyon ve belge oluşturduğumuzu bildiren bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6b386-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="6b386-196">Kod çok aşağıdaki hello eklemek**results.html** hello içinde `<body`> öğesi.</span><span class="sxs-lookup"><span data-stu-id="6b386-196">Add hello following code too**results.html** in hello `<body`> element.</span></span> <span data-ttu-id="6b386-197">Merhaba yoklama hello sonuçlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6b386-197">It displays hello results of hello poll.</span></span>
   
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
6. <span data-ttu-id="6b386-198">Kod çok aşağıdaki hello eklemek**vote.html** hello içinde `<body`> öğesi.</span><span class="sxs-lookup"><span data-stu-id="6b386-198">Add hello following code too**vote.html** in hello `<body`> element.</span></span> <span data-ttu-id="6b386-199">Merhaba yoklamayı görüntüler ve hello oyları kabul eder.</span><span class="sxs-lookup"><span data-stu-id="6b386-199">It displays hello poll and accepts hello votes.</span></span> <span data-ttu-id="6b386-200">Merhaba oy kaydetmede hello Denetim burada biz hello oy tanıyacağımız ve hello belge buna uygun olarak eklenecek tooviews.py geçirilir.</span><span class="sxs-lookup"><span data-stu-id="6b386-200">On registering hello votes, hello control is passed over tooviews.py where we will recognize hello vote cast and append hello document accordingly.</span></span>
   
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
7. <span data-ttu-id="6b386-201">Merhaba, **şablonları** klasörü Değiştir Merhaba içeriğine **index.html** hello aşağıdaki ile.</span><span class="sxs-lookup"><span data-stu-id="6b386-201">In hello **templates** folder, replace hello contents of **index.html** with hello following.</span></span> <span data-ttu-id="6b386-202">Bu, giriş sayfasında uygulamanız için hello görür.</span><span class="sxs-lookup"><span data-stu-id="6b386-202">This serves as hello landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a><span data-ttu-id="6b386-203">Bir yapılandırma dosyası ekleme ve değiştirme hello \_ \_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="6b386-203">Add a configuration file and change hello \_\_init\_\_.py</span></span>
1. <span data-ttu-id="6b386-204">Çözüm Gezgini'nde hello sağ **öğretici** projesi,'ı tıklatın **Ekle**, tıklatın **yeni öğe**seçin **boş Python dosyası**ve ardından ad hello dosyası **documentdb**.</span><span class="sxs-lookup"><span data-stu-id="6b386-204">In Solution Explorer, right-click hello **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name hello file **config.py**.</span></span> <span data-ttu-id="6b386-205">Bu yapılandırma dosyası, Flask'taki formlar için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6b386-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="6b386-206">Tooprovide gizli bir anahtar da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b386-206">You can use it tooprovide a secret key as well.</span></span> <span data-ttu-id="6b386-207">Ancak bu anahtar bu öğretici için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="6b386-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="6b386-208">Merhaba aşağıdakileri ekleyin kod tooconfig.py tooalter hello değerlerini gerekir **DOCUMENTDB\_KONAK** ve **DOCUMENTDB\_anahtar** hello sonraki adımda.</span><span class="sxs-lookup"><span data-stu-id="6b386-208">Add hello following code tooconfig.py, you'll need tooalter hello values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in hello next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="6b386-209">Merhaba, [Azure portal](https://portal.azure.com/), toohello gidin **anahtarları** dikey **Gözat**, **Azure Cosmos DB hesapları**, hello adına çift tıklayın Merhaba, toouse hesap ve hello ardından **anahtarları** hello düğmesini **Essentials** alanı.</span><span class="sxs-lookup"><span data-stu-id="6b386-209">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click hello name of hello account toouse, and then click hello **Keys** button in hello **Essentials** area.</span></span> <span data-ttu-id="6b386-210">Merhaba, **anahtarları** dikey penceresinde, kopyalama hello **URI** değer ve hello yapıştırma **documentdb** hello hello değeri olarak dosya **DOCUMENTDB\_ana bilgisayar**  özelliği.</span><span class="sxs-lookup"><span data-stu-id="6b386-210">In hello **Keys** blade, copy hello **URI** value and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="6b386-211">Hello Azure portalında, hello edilene **anahtarları** dikey penceresinde hello kopyalama hello değeri **birincil anahtar** veya hello **ikincil anahtar**ve hello yapıştırma **documentdb**  hello hello değeri olarak dosya **DOCUMENTDB\_anahtar** özelliği.</span><span class="sxs-lookup"><span data-stu-id="6b386-211">Back in hello Azure portal, in hello **Keys** blade, copy hello value of hello **Primary Key** or hello **Secondary Key**, and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="6b386-212">Merhaba,  **\_ \_init\_\_.py** dosya, aşağıdaki satırı hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6b386-212">In hello **\_\_init\_\_.py** file, add hello following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="6b386-213">Böylece hello dosyanın Merhaba içeriğine olur:</span><span class="sxs-lookup"><span data-stu-id="6b386-213">So that hello content of hello file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="6b386-214">Tüm hello dosyaları ekledikten sonra Çözüm Gezgini aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="6b386-214">After adding all hello files, Solution Explorer should look like this:</span></span>
   
    ![Merhaba Visual Studio Çözüm Gezgini penceresinin ekran görüntüsü](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="6b386-216">4. Adım: Web uygulamanızı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6b386-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="6b386-217">Tuşlarına basarak Hello çözümü derleme **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="6b386-217">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="6b386-218">Merhaba derleme başarılı olduktan sonra basarak hello Web sitesini başlatın **F5**.</span><span class="sxs-lookup"><span data-stu-id="6b386-218">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="6b386-219">Ekranda hello şunları görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b386-219">You should see hello following on your screen.</span></span>
   
    ![Ekran Merhaba Python + Azure Cosmos DB oylama bir web tarayıcısında görüntülenen uygulama görüntüsü](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="6b386-221">Tıklatın **oylama veritabanını oluştur/Temizle hello** toogenerate hello veritabanı.</span><span class="sxs-lookup"><span data-stu-id="6b386-221">Click **Create/Clear hello Voting Database** toogenerate hello database.</span></span>
   
    ![Ekran görüntüsü oluşturma sayfası'hello web uygulamasının – geliştirme ayrıntıları hello](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="6b386-223">Ardından **Oy Ver**'e tıklayın ve seçiminizi belirleyin.</span><span class="sxs-lookup"><span data-stu-id="6b386-223">Then, click **Vote** and select your option.</span></span>
   
    ![Bir oylama sorusu sorulmuş web uygulamasıyla hello ekran görüntüsü](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="6b386-225">Verdiğiniz her oy için bunu hello uygun sayaç artırılır.</span><span class="sxs-lookup"><span data-stu-id="6b386-225">For every vote you cast, it increments hello appropriate counter.</span></span>
   
    ![Hello sonuçları gösterilen hello oy sayfasının ekran görüntüsü](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="6b386-227">Shift + F5'e basarak Hello proje hata ayıklamayı durdurun.</span><span class="sxs-lookup"><span data-stu-id="6b386-227">Stop debugging hello project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-hello-web-application-tooazure"></a><span data-ttu-id="6b386-228">5. adım: hello web uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="6b386-228">Step 5: Deploy hello web application tooAzure</span></span>
<span data-ttu-id="6b386-229">Merhaba tam uygulaması düzgün çalıştığından Cosmos DB karşı sahip olduğunuza göre bu tooAzure toodeploy yapacağız.</span><span class="sxs-lookup"><span data-stu-id="6b386-229">Now that you have hello complete application working correctly against Cosmos DB, we're going toodeploy this tooAzure.</span></span>

1. <span data-ttu-id="6b386-230">Çözüm Gezgini'nde hello projeye sağ tıklayın (etmediğinizden emin olun hala yerel olarak çalışan) seçip **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="6b386-230">Right-click hello project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Çözüm Gezgini'nde hello Yayımla seçeneği vurgulanmış seçili hello Öğreticisi ekran görüntüsü](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="6b386-232">Merhaba, **Yayımla** iletişim kutusunda **Microsoft Azure App Service**seçin **Yeni Oluştur**ve ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="6b386-232">In hello **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Microsoft Azure App Service vurgulanmış hello Web'de Yayımla penceresinin ekran görüntüsü](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="6b386-234">Merhaba, **App Service Oluştur** iletişim kutusunda, web uygulamanız ile birlikte hello adını girin, **abonelik**, **kaynak grubu**, ve **App Service planı** , ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6b386-234">In hello **Create App Service** dialog box, enter hello name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Merhaba Microsoft Azure Web Apps penceresi penceresinin ekran görüntüsü](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="6b386-236">Birkaç saniye içinde Visual Studio uygulama hizmetiniz yayımlamayı bitirecek ve Azure'da çalışan, handiwork görebileceğiniz bir tarayıcıyı başlatacak!</span><span class="sxs-lookup"><span data-stu-id="6b386-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Merhaba Microsoft Azure Web Apps penceresi penceresinin ekran görüntüsü](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="6b386-238">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="6b386-238">Troubleshooting</span></span>
<span data-ttu-id="6b386-239">Bilgisayarınızda çalıştırın hello ilk Python uygulaması buysa, o hello aşağıdakilerden emin olun klasörlerin (veya hello eşdeğer yükleme konumlarının) yol değişkeninize bulunmaktadır:</span><span class="sxs-lookup"><span data-stu-id="6b386-239">If this is hello first Python app you've run on your computer, ensure that hello following folders (or hello equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="6b386-240">Oy sayfanızda bir hata alırsanız ve projenize bir şey dışında adlı **öğretici**, olduğundan emin olun  **\_ \_init\_\_.py** başvuruları hello hello satır doğru proje adına: `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="6b386-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references hello correct project name in hello line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b386-241">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b386-241">Next steps</span></span>
<span data-ttu-id="6b386-242">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="6b386-242">Congratulations!</span></span> <span data-ttu-id="6b386-243">Yalnızca Cosmos DB kullanarak ilk Python web uygulamanızı tamamladınız ve tooAzure yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="6b386-243">You have just completed your first Python web application using Cosmos DB and published it tooAzure.</span></span>

<span data-ttu-id="6b386-244">Geri bildirimlerinizi temel alarak bu konu başlığını sıklıkla güncelleştirip iyileştiriyoruz.</span><span class="sxs-lookup"><span data-stu-id="6b386-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="6b386-245">Bir kez hello öğretici, lütfen oylama düğmeleri hello en üstündeki ve bu sayfanın hello tamamladıktan ve yapılan toosee istediğiniz hangi iyileştirmeler hakkında geri bildirim emin tooinclude olabilir.</span><span class="sxs-lookup"><span data-stu-id="6b386-245">Once you've completed hello tutorial, please using hello voting buttons at hello top and bottom of this page, and be sure tooinclude your feedback on what improvements you want toosee made.</span></span> <span data-ttu-id="6b386-246">Bize istiyorsanız toocontact doğrudan düşündüğünüz e-posta adresi serbest tooinclude yorumlarınızı içinde.</span><span class="sxs-lookup"><span data-stu-id="6b386-246">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="6b386-247">tooadd ek işlevler tooyour web uygulaması, gözden geçirme hello API'leri hello kullanılabilir [Azure Cosmos DB Python SDK'sı](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="6b386-247">tooadd additional functionality tooyour web application, review hello APIs available in hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="6b386-248">Azure, Visual Studio ve Python hakkında daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="6b386-248">For more information about Azure, Visual Studio, and Python, see hello [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="6b386-249">Ek Python Flask öğreticileri için bkz: [hello büyük Flask Öğreticisi, bölümü I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span><span class="sxs-lookup"><span data-stu-id="6b386-249">For additional Python Flask tutorials, see [hello Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
