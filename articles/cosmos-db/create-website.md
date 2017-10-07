---
title: "bir web uygulaması şablonu - Azure Cosmos DB ile aaaDeploy | Microsoft Docs"
description: "Nasıl toodeploy Azure Cosmos DB hesabı, Azure App Service Web Apps ve örnek bir web uygulaması bir Azure Resource Manager şablonu kullanarak öğrenin."
services: cosmos-db, app-service\web
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 087d8786-1155-42c7-924b-0eaba5a8b3e0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b2bdde9279aad570606d7bf06dfc710f564b4d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a>Azure Cosmos DB ve Azure App Service Web Apps bir Azure Resource Manager şablonu kullanarak dağıtın
Bu öğretici şunların nasıl yapıldığını gösterir toouse bir Azure Resource Manager şablonu toodeploy ve tümleştirme [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), bir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web uygulaması ve bir örnek web uygulaması.

Azure Resource Manager şablonları kullanarak hello dağıtımını ve yapılandırmasını Azure kaynaklarınızı kolayca otomatikleştirebilirsiniz.  Bu öğreticide gösterilmiştir nasıl toodeploy bir web uygulaması ve otomatik olarak Azure Cosmos DB hesap bağlantı bilgilerini yapılandırın.

Bu öğreticiyi tamamladıktan sonra aşağıdaki soruları mümkün tooanswer hello olacaktır:  

* Nasıl bir Azure Resource Manager şablonu toodeploy kullanın ve Azure Cosmos DB hesabınız ve Azure App Service'te bir web uygulaması tümleştirme?
* Nasıl bir Azure Resource Manager şablonu toodeploy kullanın ve Azure Cosmos DB hesabınız, App Service Web Apps bir web uygulamasını ve Webdeploy uygulama tümleştirme?

<a id="Prerequisites"></a>

## <a name="prerequisites"></a>Ön koşullar
> [!TIP]
> Bu öğreticide Azure Resource Manager şablonları veya JSON konusunda deneyim varsaymaz olsa da, şablonları ya da dağıtım seçenekleri toomodify hello başvurulan sonra bu alanlardan her birini bilgisi gerekli olacak istediğiniz.
> 
> 

Bu öğreticide Hello yönergeleri izlemeden önce hello aşağıdaki sahip olduğundan emin olun:

* Azure aboneliği. Azure abonelik tabanlı bir platformdur.  Bir aboneliği edinme hakkında daha fazla bilgi için bkz: [satın alma seçenekleri](https://azure.microsoft.com/pricing/purchase-options/), [üye teklifleri](https://azure.microsoft.com/pricing/member-offers/), veya [ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/).

## <a id="CreateDB"></a>1. adım: hello şablon dosyalarını indirme
Bu öğreticide kullanacağız hello şablon dosyalarını yükleyerek başlayalım.

1. Merhaba karşıdan [Azure Cosmos DB hesap, Web uygulamaları oluşturmak ve bir gösterim uygulama örneği dağıtma](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) şablonu tooa yerel klasöre (örneğin C:\Azure Cosmos DBTemplates). Bu şablon, bir Azure Cosmos DB hesabı, bir App Service web uygulaması ve bir web uygulamasına dağıtır.  Ayrıca, hello web uygulama tooconnect toohello Azure Cosmos DB hesabı da otomatik olarak yapılandırır.
2. Merhaba karşıdan [bir Azure Cosmos DB hesap ve Web uygulamaları örnek oluşturma](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) şablonu tooa yerel klasöre (örneğin C:\Azure Cosmos DBTemplates). Bu şablon, bir App Service web uygulaması Azure Cosmos DB hesap dağıtır ve hello sitenin uygulama ayarlarını tooeasily yüzey Azure Cosmos DB bağlantısı bilgilerini değiştirir, ancak bir web uygulaması içermez.  

<a id="Build"></a>

## <a name="step-2-deploy-hello-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a>Adım 2: hello Azure Cosmos DB hesap dağıtma App Service web uygulaması ve tanıtım uygulama örneği
Şimdi şimdi bizim ilk şablonunu dağıtın.

> [!TIP]
> Merhaba şablon hello web uygulaması adı ve Azure Cosmos DB hesap adı altında girilen bir) geçerli ve (b) kullanılabilir olduğundan doğrulamaz.  Merhaba hello kullanılabilirliğini adlarını doğrulayın önerilen planlama toosupply önceki toosubmitting hello dağıtım.
> 
> 

1. Oturum açma toohello [Azure Portal](https://portal.azure.com), yeni'yi tıklatın ve "Şablon dağıtımı" için arama yapın.
    ![Merhaba şablon dağıtımı kullanıcı Arabirimi ekran görüntüsü](./media/create-website/TemplateDeployment1.png)
2. Merhaba şablon dağıtımı öğeyi seçin ve tıklatın **oluşturma** ![hello şablon dağıtımı kullanıcı Arabirimi ekran görüntüsü](./media/create-website/TemplateDeployment2.png)
3. Tıklatın **Düzen şablonu**hello hello DocDBWebsiteTodo.json şablon dosyasının içeriğini yapıştırın ve tıklatın **kaydetmek**.
   ![Merhaba şablon dağıtımı kullanıcı Arabirimi ekran görüntüsü](./media/create-website/TemplateDeployment3.png)
4. Tıklatın **Düzenle parametreleri**, her hello zorunlu parametreler için değerler sağlayın ve tıklayın **Tamam**.  Merhaba parametreleri aşağıdaki gibidir:
   
   1. SITENAME: hello App Service web uygulaması adı belirtir ve kullanılan tooconstruct hello URL'si tooaccess hello web uygulama kullanır (örneğin "mydemodocdbwebapp" belirttiğiniz sonra hello URL olarak, erişim hello web uygulaması olacaktır mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: App Service planı toocreate barındırma hello adını belirtir.
   3. KONUMU: Belirtir toocreate hello Azure Cosmos DB ve web uygulama kaynakları Azure konumda hello.
   4. DATABASEACCOUNTNAME: hello Azure Cosmos DB hesap toocreate hello adını belirtir.   
      
      ![Merhaba şablon dağıtımı kullanıcı Arabirimi ekran görüntüsü](./media/create-website/TemplateDeployment4.png)
5. Varolan bir kaynak grubu seçin veya yeni bir kaynak grubu adı toomake sağlayın ve hello kaynak grubu için bir konum seçin.

    ![Merhaba şablon dağıtımı kullanıcı Arabirimi ekran görüntüsü](./media/create-website/TemplateDeployment5.png)
6. Tıklatın **yasal koşulları gözden geçir**, **satın alma**ve ardından **oluşturma** toobegin hello dağıtım.  Seçin **PIN toodashboard** hello elde edilen dağıtımı Azure portal giriş sayfasında kolayca görünür olacak şekilde.
   ![Merhaba şablon dağıtımı kullanıcı Arabirimi ekran görüntüsü](./media/create-website/TemplateDeployment6.png)
7. Merhaba dağıtım sona erdiğinde, hello kaynak grubu dikey pencere açılır.
   ![Merhaba kaynak grubu dikey penceresinin ekran görüntüsü](./media/create-website/TemplateDeployment7.png)  
8. toouse Merhaba uygulama, sadece toohello web uygulaması URL'si gidin (Merhaba yukarıdaki örnekte, http://mydemodocdbwebapp.azurewebsites.net hello URL'si olacaktır).  Web uygulama aşağıdaki hello görürsünüz:
   
   ![Örnek Todo uygulaması](./media/create-website/image2.png)
9. Devam edin ve birkaç görevleri hello web uygulaması oluşturmak ve hello Azure portal toohello kaynak grubu dikey penceresine dönün. Hello Azure Cosmos DB hesap kaynağında hello kaynaklar listesine tıklayın ve ardından **sorgu Gezgini**.
    ![Ekran görüntüsü hello özeti Mercek vurgulanmış hello web uygulaması](./media/create-website/TemplateDeployment8.png)  
10. Merhaba varsayılan sorguyu çalıştırma "seçin * c" ve hello sonuçlarını inceleyin.  Merhaba sorgulayan alınan hello JSON gösterimi, yukarıdaki 7. adımda oluşturduğunuz hello Yapılacaklar öğelerinin dikkat edin.  Ücretsiz tooexperiment sorgularla eşitleyerek; Örneğin, SELECT çalıştırmayı deneyin * c WHERE c.isComplete = true tooreturn tamamlandı olarak işaretlenmiş tüm yapılacaklar öğelerini.
    
    ![Merhaba sorgu Gezgini ve sonuçları dikey pencereleri hello sorgu sonuçlarını gösteren ekran görüntüsü](./media/create-website/image5.png)
11. Ücretsiz tooexplore hello Azure Cosmos DB portal deneyimi eşitleyerek veya Merhaba örnek Todo uygulaması değiştirin.  Hazır olduğunuzda, şirketinizdeki başka bir şablonu dağıtın.

<a id="Build"></a> 

## <a name="step-3-deploy-hello-document-account-and-web-app-sample"></a>Adım 3: hello belge hesabı ve web uygulaması örneği dağıtma
Şimdi şimdi bizim ikinci şablonunu dağıtın.  Bu şablon yararlı tooshow nasıl, uygulama ayarları veya özel bağlantı dizesi olarak bir web uygulamasına Azure Cosmos DB bağlantısı bilgilerini hesap uç noktası ve ana anahtar gibi ekleyemezsiniz. Örneğin, kendi web uygulaması, bir Azure Cosmos DB hesapla toodeploy ister ve dağıtım sırasında otomatik olarak doldurulur hello bağlantı bilgilerini sahip sahip belki de.

> [!TIP]
> Merhaba şablon hello web uygulaması adı ve Azure Cosmos DB hesap adı altında girilen bir) geçerli ve (b) kullanılabilir olduğundan doğrulamaz.  Merhaba hello kullanılabilirliğini adlarını doğrulayın önerilen planlama toosupply önceki toosubmitting hello dağıtım.
> 
> 

1. Merhaba, [Azure Portal](https://portal.azure.com), yeni'yi tıklatın ve "Şablon dağıtımı" için arama yapın.
    ![Merhaba şablon dağıtımı kullanıcı Arabirimi ekran görüntüsü](./media/create-website/TemplateDeployment1.png)
2. Merhaba şablon dağıtımı öğeyi seçin ve tıklatın **oluşturma** ![hello şablon dağıtımı kullanıcı Arabirimi ekran görüntüsü](./media/create-website/TemplateDeployment2.png)
3. Tıklatın **Düzen şablonu**hello hello DocDBWebSite.json şablon dosyasının içeriğini yapıştırın ve tıklatın **kaydetmek**.
   ![Merhaba şablon dağıtımı kullanıcı Arabirimi ekran görüntüsü](./media/create-website/TemplateDeployment3.png)
4. Tıklatın **Düzenle parametreleri**, her hello zorunlu parametreler için değerler sağlayın ve tıklayın **Tamam**.  Merhaba parametreleri aşağıdaki gibidir:
   
   1. SITENAME: hello App Service web uygulaması adı belirtir ve kullanılan tooconstruct hello URL'si tooaccess hello web uygulama kullanır (örneğin "mydemodocdbwebapp" belirttiğiniz sonra hello URL olarak, erişim hello web uygulaması olacaktır mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: App Service planı toocreate barındırma hello adını belirtir.
   3. KONUMU: Belirtir toocreate hello Azure Cosmos DB ve web uygulama kaynakları Azure konumda hello.
   4. DATABASEACCOUNTNAME: hello Azure Cosmos DB hesap toocreate hello adını belirtir.   
      
      ![Merhaba şablon dağıtımı kullanıcı Arabirimi ekran görüntüsü](./media/create-website/TemplateDeployment4.png)
5. Varolan bir kaynak grubu seçin veya yeni bir kaynak grubu adı toomake sağlayın ve hello kaynak grubu için bir konum seçin.

    ![Merhaba şablon dağıtımı kullanıcı Arabirimi ekran görüntüsü](./media/create-website/TemplateDeployment5.png)
6. Tıklatın **yasal koşulları gözden geçir**, **satın alma**ve ardından **oluşturma** toobegin hello dağıtım.  Seçin **PIN toodashboard** hello elde edilen dağıtımı Azure portal giriş sayfasında kolayca görünür olacak şekilde.
   ![Merhaba şablon dağıtımı kullanıcı Arabirimi ekran görüntüsü](./media/create-website/TemplateDeployment6.png)
7. Merhaba dağıtım sona erdiğinde, hello kaynak grubu dikey pencere açılır.
   ![Merhaba kaynak grubu dikey penceresinin ekran görüntüsü](./media/create-website/TemplateDeployment7.png)  
8. Merhaba Web uygulaması kaynak hello kaynaklar listesine tıklayın ve ardından **uygulama ayarları** ![hello kaynak grubunun ekran görüntüsü](./media/create-website/TemplateDeployment9.png)  
9. Nasıl uygulama ayarları hello Azure Cosmos DB uç noktası ve her hello Azure Cosmos DB ana anahtarları için mevcut dikkat edin.

    ![Uygulama ayarları ekran görüntüsü](./media/create-website/TemplateDeployment10.png)  
10. Hello Azure Portal keşfetme ücretsiz toocontinue eşitleyerek veya bizim Azure Cosmos DB birini izleyin [örnekleri](http://go.microsoft.com/fwlink/?LinkID=402386) toocreate kendi Azure Cosmos DB uygulama.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Sonraki adımlar
Tebrikler! Azure Cosmos DB, App Service web uygulaması ve Azure Resource Manager şablonları kullanarak örnek bir web uygulamasına dağıttıktan sonra.

* Azure Cosmos DB hakkında daha fazla toolearn tıklatın [burada](http://azure.com/docdb).
* Azure App Service Web apps hakkında daha fazla toolearn tıklatın [burada](http://go.microsoft.com/fwlink/?LinkId=325362).
* Azure Resource Manager şablonları hakkında daha fazla toolearn tıklatın [burada](https://msdn.microsoft.com/library/azure/dn790549.aspx).

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)
* Yeni portalı eski portal toohello hello değişikliği Kılavuzu toohello için bkz: [gezinme için başvuru hello Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkId=529715)

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](http://go.microsoft.com/fwlink/?LinkId=523751), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

