---
title: "aaaCreate hello Azure SDK'sı için Java kullanarak Azure App Service Web uygulamasında"
description: "Nasıl toocreate program aracılığıyla kullanarak Azure App Service'te bir Web uygulaması hello Java için Azure SDK'sı hakkında bilgi edinin."
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a>Java için hello Azure SDK kullanarak Azure App Service Web uygulaması oluşturma
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl gösterir toocreate bir Web uygulamasını oluşturan bir Java uygulamanız için bir Azure SDK [Azure App Service][Azure App Service], bir uygulama tooit dağıtın. İki bölümden oluşur:

* Bölüm 1 nasıl bir web uygulamasını oluşturur toobuild bir Java uygulaması gösterir.
* 2. Bölüm gösterir nasıl toocreate basit bir JSP "Hello World" uygulaması, sonra kullanım bir FTP istemcisi toodeploy kod tooApp hizmet.

## <a name="prerequisites"></a>Ön koşullar
### <a name="software-installations"></a>Yazılım yüklemeleri
Merhaba AzureWebDemo uygulama kodu bu makalede, Azure Java kullanarak yükleyebileceğiniz SDK 0.7.0, kullanarak yazıldı hello [Web Platformu yükleyicisi] [ Web Platform Installer] (Webpı). Ayrıca, emin toouse hello en son sürümünü hello olun [Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]. Çalıştırarak Eclipse projenizin hello bağımlılıkları hello SDK yükledikten sonra güncelleştirme **güncelleştirme dizin** içinde **Maven depoları**, hello hello her paketi en son sürümünü yeniden ekleyin  **Bağımlılıklar** penceresi. Eclipse'te yüklü yazılım hello sürümü tıklatarak doğrulayabilirsiniz **Yardım > Yükleme ayrıntıları**; size sahip en az hello sürümler:

* Microsoft Azure kitaplıkları için Java 0.7.0.20150309 paketi
* Java EE geliştiricileri 4.4.2.20150219 için Eclipse IDE

### <a name="create-and-configure-cloud-resources-in-azure"></a>Oluşturma ve Azure içinde bulut kaynaklarını yapılandırma
Bu yordama başlamadan önce toohave etkin bir Azure aboneliği gerekir ve varsayılan Active Directory (AD) Azure üzerinde ayarlayın.

### <a name="create-an-active-directory-ad-in-azure"></a>Bir Active Directory (AD) oluşturma
Bir Active Directory (AD), Azure aboneliğinizde zaten yoksa, hello oturum [Klasik Azure portalı] [ Azure classic portal] Microsoft hesabınızla. Birden çok aboneliğiniz varsa, tıklatın **abonelikleri** ve select hello varsayılan dizin hello abonelik için bu proje için toouse istiyor. Ardından **Uygula** tooswitch toothat abonelik görünümü.

1. Seçin **Active Directory** sol hello menüden. **Yeni tıklayın > Dizin > özel Oluştur**.
2. İçinde **Dizin Ekle**seçin **yeni dizin oluştur**.
3. İçinde **adı**, bir dizin adı girin.
4. İçinde **etki alanı**, bir etki alanı adı girin. Bu dizin ile varsayılan olarak bulunan bir temel etki alanı adıdır; Merhaba form sahip `<domain_name>.onmicrosoft.com`. Örneğin hello dizin adı veya sahip olduğunuz başka bir etki alanı adını temel alarak adı verebilirsiniz. Daha sonra kuruluşunuzun zaten kullanan başka bir etki alanı adı ekleyebilirsiniz.
5. İçinde **ülke veya bölge**, bölgeniz seçin.

AD hakkında daha fazla bilgi için bkz: [Azure AD dizini nedir][What is an Azure AD directory]?

### <a name="create-a-management-certificate-for-azure"></a>Azure için bir yönetim sertifikası oluşturun
Merhaba Java için Azure SDK'sı Azure abonelikleri ile yönetim sertifikaları tooauthenticate kullanır. X.509 v3 sertifikaları tooauthenticate hello abonelik sahibi toomanage abonelik kaynakları adına hello Hizmet Yönetimi API'si tooact kullanan bir istemci uygulaması kullandığınız bunlar.

Bu yordamdaki Hello kod Azure ile otomatik olarak imzalanan sertifika tooauthenticate kullanır. Bu yordam için toocreate bir sertifika gerekir ve toohello karşıya [Klasik Azure portalı] [ Azure classic portal] önceden. Merhaba aşağıdaki adımları içerir:

* İstemci sertifikanızın temsil eden bir PFX dosyası oluşturma ve yerel olarak kaydedin.
* Merhaba PFX dosyasından bir yönetim sertifikası (CER dosyası) oluşturur.
* Merhaba CER dosyasını tooyour Azure aboneliği karşıya yükleyin.
* Java sertifikaları kullanarak bu biçimi tooauthenticate kullandığından hello PFX dosyasını JKS dönüştürün.
* Toohello yerel JKS dosyası başvuruyor hello uygulamanın kimlik doğrulama kodu yazın.

Bu yordamı tamamladıktan sonra hello CER sertifika Azure aboneliğinizde yer alacağını ve hello JKS sertifika yerel diskinize yer alacağı. Yönetim sertifikaları hakkında daha fazla bilgi için bkz: [oluşturun ve Azure için yönetim sertifikası karşıya][Create and Upload a Management Certificate for Azure].

#### <a name="create-a-certificate"></a>Sertifika oluşturma
toocreate kendi otomatik olarak imzalanan sertifika, işletim sisteminde bir komut konsolunu açın ve hello aşağıdaki komutları çalıştırın.

> **Not:** bu komutu çalıştırdığınız hello bilgisayarın hello JDK yüklü olması gerekir. Ayrıca, hello yolu toohello keytool hello JDK yüklemek hello konumuna bağlıdır. Daha fazla bilgi için bkz: [anahtar ve Sertifika Yönetim Aracı (keytool)] [ Key and Certificate Management Tool (keytool)] hello Java çevrimiçi belgeleri içinde.
> 
> 

toocreate hello .pfx dosyası:

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

toocreate hello .cer dosyası:

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

Burada:

* `<java-install-dir>`Java yüklü hello yolu toohello dizinidir.
* `<keystore-id>`Merhaba bir anahtar girişi tanımlayıcıdır (örneğin, `AzureRemoteAccess`).
* `<cert-store-dir>`toostore sertifikaları istediğiniz hello yolu toohello dizin (örneğin `C:/Certificates`).
* `<cert-file-name>`Merhaba hello sertifika dosyasının adıdır (örneğin `AzureWebDemoCert`).
* `<password>`Merhaba'a kadar olan tooprotect hello sertifika seçtiğiniz paroladır; en az 6 karakter uzunluğunda olmalıdır. Önerilmemesine rağmen bir parola girebilirsiniz.
* `<dname>`Merhaba X.500 ayırt edici ad toobe diğer ad ile ilişkili olan ve hello veren ve hello otomatik olarak imzalanan sertifika konu alanları olarak kullanılır.

Daha fazla bilgi için bkz: [oluşturun ve Azure için yönetim sertifikası karşıya][Create and Upload a Management Certificate for Azure].

#### <a name="upload-hello-certificate"></a>Merhaba sertifikasını karşıya yükle
tooupload otomatik olarak imzalanan sertifika tooAzure gidin toohello **ayarları** sayfasında hello Klasik Portalı'nda ve ardından hello **yönetim sertifikaları** sekmesi. Tıklatın **karşıya** hello hello sonundaki sayfasında ve oluşturduğunuz hello CER dosyasını toohello konumuna gidin.

#### <a name="convert-hello-pfx-file-into-jks"></a>Merhaba PFX dosyasının JKS Dönüştür
Hello Windows komut istemi (yönetici olarak çalışır), cd toohello dizinini içeren hello sertifikaları ve komut, aşağıdaki hello çalıştırmak nerede `<java-install-dir>` yüklediğiniz Java bilgisayarınızda hello dizindir:

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. İstendiğinde, hello hedef anahtar deposu parolasını girin; Bu hello JKS dosyası hello parolası olacaktır.
2. İstendiğinde, hello kaynağı anahtar deposu parolasını girin; Bu hello PFX dosyası için belirtilen hello paroladır.

Merhaba iki parola aynı hello toobe gerekmez. Önerilmemesine rağmen bir parola girebilirsiniz.

## <a name="build-a-web-app-creation-application"></a>Bir Web uygulaması oluşturma uygulaması oluşturma
### <a name="create-hello-eclipse-workspace-and-maven-project"></a>Oluşturma Eclipse çalışma alanında ve bir Maven projesi hello
Bu bölümde bir çalışma alanı ve AzureWebDemo adlı hello web uygulaması oluşturma uygulaması için bir Maven projesi oluşturun.

1. Yeni bir Maven projesi oluşturun. Tıklatın **Dosya > Yeni > Maven projesine**. İçinde **yeni bir Maven projesi**seçin **basit bir proje oluşturun** ve **varsayılan çalışma alanı konumu kullanacak**.
2. Merhaba ikinci sayfasında **yeni bir Maven projesi**, hello aşağıdakileri belirtin:
   
   * Grup Kimliği:`com.<username>.azure.webdemo`
   * Artifact ID: AzureWebDemo
   * Sürüm: 0.0.1-SNAPSHOT
   * Paketleme: jar
   * Ad: AzureWebDemo
     
     **Son**'a tıklayın.
3. Proje Gezgini'nde Hello yeni projenin pom.xml dosyasını açın. Select hello **bağımlılıkları** sekmesi. Yeni bir proje olarak hiç paket henüz listelenir.
4. Açık hello Maven depoları görüntüleyin. **Pencere tıklayın > Görünümü Göster > Diğer > Maven > Maven depoları** tıklatıp **Tamam**. Merhaba **Maven depoları** görünüm hello IDE hello alt kısmında görüntülenir.
5. Açık **genel depoları**, sağ hello **Merkezi** depo ve select **yeniden dizin**.
   
    ![][1]
   
    Bu adım hello bağlantınızın hızına bağlı olarak birkaç dakika sürebilir. Merhaba dizini yeniden oluşturur, hello hello Microsoft Azure paketlerinde görmelisiniz **Merkezi** Maven deposu.
6. İçinde **bağımlılıkları**, tıklatın **Ekle**. İçinde **grubu kimliği girin...**  girin `azure-management`. Temel ve App Service Web Apps Yönetimi Hello paketlerini seçin:
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > **Not:** sonra yeni bir sürüm yayın hello bağımlılıkları güncelleştiriyorsanız toore gereksinim-her hello bağımlılıkları bu listeye ekleyin.
   > Tıklattıktan sonra **Ekle** ve hello yeni sürüm numarasıyla hello olarak göründüğü her bir bağımlılığın seçin **bağımlılıkları** listesi.
   > 
   > 

**Tamam** düğmesine tıklayın. Azure paketleri hello sonra hello görünür **bağımlılıkları** listesi.

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a>Java kod tooCreate arama hello Azure SDK'sı tarafından bir Web uygulaması yazma
Ardından, Java toocreate hello App Service web uygulaması hello Azure SDK'sı API'lerini çağırır hello kodu yazın.

1. Bir Java sınıfı toocontain hello ana giriş noktası kodu oluşturun. Proje Gezgini'nde hello proje düğümüne sağ tıklayın ve seçin **yeni > sınıfı**.
2. İçinde **yeni Java sınıfı**, ad hello sınıfı `WebCreator` ve hello denetleyin **ortak statik void ana** onay kutusu. Merhaba seçimleri aşağıdaki gibi görünmelidir:
   
    ![][2]
3. **Son**'a tıklayın. Merhaba WebCreator.java dosyası proje Gezgini'nde görünür.

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a>Bir App Service Web uygulaması Hello Azure API tooCreate çağırma
#### <a name="add-necessary-imports"></a>Gerekli içeri aktarmaları ekleyin
WebCreator.java içinde hello aşağıdaki içeri aktarmaları ekleyin; Bu içeri aktarmalar erişim tooclasses hello içinde Azure API'lerini kullanan yönetim kitaplıkları sağlar:

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-hello-main-entry-point-class"></a>Merhaba ana giriş noktası sınıf tanımlama
Merhaba AzureWebDemo uygulama Hello amacı toocreate bir App Service Web uygulaması olduğundan, bu uygulama için hello ana sınıf adını `WebAppCreator`. Bu sınıf hello Azure Hizmet Yönetimi API toocreate hello web uygulamasını çağıran hello ana giriş noktası kodu sağlar.

Parametre tanımları hello web uygulaması ve Web alanı için aşağıdaki hello ekleyin. Kendi Azure abonelik kimliği ve sertifika bilgilerini tooprovide gerekir.

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

Burada:

* `<subscription-id>`toocreate hello kaynak istediğiniz hello Azure abonelik kimliği değil.
* `<certificate-store-path>`Merhaba yol ve dosya adı toohello JKS yerel sertifika deposu dizininizde dosyasıdır. Örneğin, `C:/Certificates/CertificateName.jks` Linux için ve `C:\Certificates\CertificateName.jks` Windows için.
* `<certificate-password>`Merhaba'a kadar olan JKS sertifikanızı oluştururken belirttiğiniz paroladır.
* `webAppName`Seçtiğiniz herhangi bir ad olabilir; Bu yordam hello adı kullanır `WebDemoWebApp`. Merhaba tam etki alanı adıdır hello `webAppName` hello ile `domainName` eklenir, bu durumda hello tam etki alanı içinde `webdemowebapp.azurewebsites.net`.
* `domainName`yukarıda gösterildiği gibi belirtilmesi gerekir.
* `webSpaceName`hello tanımlanan hello değerlerinden biri olmalıdır [WebSpaceNames] [ WebSpaceNames] sınıfı.
* `appServicePlanName`yukarıda gösterildiği gibi belirtilmesi gerekir.

> **Not:** her zaman bu uygulamayı çalıştırmak, toochange hello değerini gerek `webAppName` ve `appServicePlanName` (veya hello Azure Portal hello web uygulamasını silmek) hello uygulamayı yeniden çalıştırmadan önce. Aksi takdirde Hello aynı kaynak Azure üzerinde zaten olduğundan yürütme başarısız olur.
> 
> 

#### <a name="define-hello-web-creation-method"></a>Merhaba web oluşturma yöntemini tanımlayın
Ardından, bir yöntem toocreate hello web uygulaması tanımlayın. Bu yöntem `createWebApp`, hello web app ve hello Web alanı hello parametreleri belirtir. Ayrıca oluşturur ve hello tarafından tanımlanan hello App Service Web Apps yönetim istemcisini yapılandırır [WebSiteManagementClient] [ WebSiteManagementClient] nesnesi. anahtar toocreating Web Apps Hello yönetim istemcidir. Merhaba Hizmet Yönetimi API'sini çağırarak web uygulamaları (oluşturmak gibi güncelleştirme ve silme işlemlerini gerçekleştirme) uygulamaları toomanage izin RESTful web hizmetleri sağlar.

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

Merhaba kod hello HTTP durum başarı veya başarısızlık belirten hello yanıtının çıkarır ve başarılı olursa, web uygulaması oluşturuldu hello hello adını çıkarır.

#### <a name="define-hello-main-method"></a>Merhaba main() yöntemi tanımlayın
Merhaba main() yönteminin kodu bu çağrıları createWebApp() toocreate hello web uygulaması sağlar.

Son olarak, arama `createWebApp` gelen `main`:

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a>Merhaba uygulamayı çalıştırın ve web uygulaması oluşturma doğrulayın
Uygulamanızı çalıştıran, tooverify tıklatın **Çalıştır > Çalıştır**. Merhaba uygulaması çalışıyor tamamlandığında, çıkış hello Eclipse konsolunda aşağıdaki hello görmeniz gerekir:

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

Klasik Azure portalı hello oturum ve'ı tıklatın **Web Apps**. Hello yeni web uygulaması, birkaç dakika içinde hello Web uygulamaları listesinde görüntülenmelidir.

## <a name="deploying-an-application-toohello-web-app"></a>Bir uygulama toohello Web uygulaması dağıtma
AzureWebDemo çalıştırıp hello yeni web uygulaması, hello Klasik portal günlüğüne oluşturulan tıklatın sonra **Web Apps**seçip **WebDemoWebApp** hello içinde **Web Apps** listesi. Merhaba web uygulamanızın panosu sayfasında tıklatın **Gözat** (veya hello URL'yi tıklatın `webdemowebapp.azurewebsites.net`) toonavigate tooit. İçerik yayımlanan toohello web uygulaması henüz bırakıldığından boş yer tutucu sayfasını görürsünüz.

Sonraki bir "Hello World" uygulaması oluşturacak ve toohello web uygulaması dağıtma.

### <a name="create-a-jsp-hello-world-application"></a>JSP Merhaba Dünya uygulaması oluşturma
#### <a name="create-hello-application"></a>Merhaba uygulaması oluşturma
Nasıl toodeploy bir uygulama toohello web hello sipariş toodemonstrate içinde aşağıdaki yordamı, nasıl gösterir toocreate basit bir "Hello World" Java uygulaması ve Web uygulamanızı oluşturduğunuz uygulama hizmeti toohello yükleyin.

1. Tıklatın **Dosya > Yeni > Dinamik Web projesi**. Bunu, `JSPHello` olarak adlandırın. Bu iletişim kutusunda herhangi bir ayarı toochange gerekmez. **Son**'a tıklayın.
   
    ![][3]
2. Proje Gezgini'nde hello genişletin **JSPHello** projesinde **WebContent**, ardından **yeni > JSP dosyası**. Merhaba yeni JSP dosyası iletişim kutusunda, hello yeni dosya adı `index.jsp`. **İleri**’ye tıklayın.
3. Merhaba, **JSP şablon seç** iletişim kutusunda **yeni JSP dosyası (html)** tıklatıp **son**.
4. İndex.jsp içinde hello kodda aşağıdaki hello eklemek `<head>` ve `<body>` etiketi bölümler:
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a>İçinde localhost Hello Hello World uygulamayı çalıştırın
Bu uygulamayı çalıştırmadan önce birkaç özelliği tooconfigure gerekir.

1. Sağ hello **JSPHello** proje ve seçin **özellikleri**.
2. Merhaba, **özellikleri** iletişim: seçin **Java oluşturma yolu**seçin hello **sipariş ve dışarı aktarma** sekmesi, onay **JRE sistem kitaplığı**,'ye tıklayın **Yukarı** toomove onu hello listenin toohello.
   
    ![][4]
3. Merhaba, ayrıca **özellikleri** iletişim: seçin **hedeflenen çalışma zamanları** tıklatıp **yeni**.
4. Merhaba, **yeni sunucu çalışma zamanı ortamı** iletişim, sunucusu gibi bir seçin **Apache Tomcat v7.0** tıklatıp **sonraki**. Merhaba, **Tomcat sunucusunu** iletişim, kümesi **adı** çok`Apache Tomcat v7.0`ve ayarlayın **Tomcat yükleme dizinini** toohello directory hello sürümü yüklü Tomcat sunucusunu toouse istiyor.
   
    ![][5]
   
    **Son**'a tıklayın.
5. Toohello sonra geri dönüp **hedeflenen çalışma zamanları** hello sayfasının **özellikleri** iletişim. Seçin **Apache Tomcat v7.0**, ardından **Tamam**.
   
    ![][6]
6. Merhaba Eclipse içinde **çalıştırmak** menüsünde tıklatın **çalıştırmak**. Merhaba, **Çalıştır** iletişim kutusunda **sunucu üzerinde çalışan**. Merhaba, **sunucu üzerinde çalışan** iletişim kutusunda **Tomcat v7.0 sunucusu**:
   
    ![][7]
   
    **Son**'a tıklayın.
7. Olduğunda, uygulama çalıştığında Merhaba, hello görmelisiniz **JSPHello** sayfa görünür Eclipse localhost penceresinde (`http://localhost:8080/JSPHello/`), görüntüleme hello ileti:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a>Merhaba uygulaması bir WAR olarak dışarı aktarma
Böylece toohello web uygulaması dağıtma hello web projesi dosyaları web arşivi (WAR) dosyası dışarı aktarın. Merhaba aşağıdaki web projesi dosyaları hello WebContent klasöründe bulunur:

    META-INF
    WEB-INF
    index.jsp

1. Merhaba WebContent klasörünü sağ tıklatın ve seçin **verme**.
2. Merhaba, **ver'i seçin** iletişim kutusunda, tıklatın **Web > WAR** dosya ve ardından **sonraki**.
3. Merhaba, **WAR dışarı** iletişim kutusunda, hello geçerli projede hello src dizin seçin ve hello WAR dosyasını hello sonunda hello adını içerir. Örneğin:
   
    `<project-path>/JSPHello/src/JSPHello.war`

WAR dosyaları dağıtma hakkında daha fazla bilgi için bkz: [bir Java uygulaması tooAzure App Service Web Apps eklemek](web-sites-java-add-app.md).

### <a name="deploying-hello-hello-world-application-using-ftp"></a>Merhaba Hello World uygulama kullanarak FTP dağıtma
Bir üçüncü taraf FTP istemcisi toopublish hello uygulaması'nı seçin. Bu yordam, iki seçenek açıklar: Azure'da; yerleşik hello Kudu konsol ve FileZilla, kolay ve grafik kullanıcı Arabirimi ile popüler bir araç.

> **Not:** Azure Araç Seti hello Eclipse destekleyen dağıtım toostorage hesapları ve bulut Hizmetleri, ancak şu anda dağıtım tooweb uygulamaları desteklemez. Toostorage hesapları dağıtmayı ve bulut hizmetlerini açıklandığı gibi Azure dağıtım projesi kullanarak [bir Hello World uygulamasının Azure için Eclipse'te oluşturma](http://msdn.microsoft.com/library/azure/hh690944.aspx), ancak değil tooweb uygulamalar. FTP veya GitHub tootransfer dosyaları tooyour web uygulaması gibi diğer yöntemleri kullanın.
> 
> **Not:** hello Windows komut isteminde (Windows ile birlikte gelen hello komut satırı FTP.EXE yardımcı programı) FTP kullanmanızı önermiyoruz. FTP.EXE gibi etkin FTP Kullan FTP istemcileri, güvenlik duvarları toowork sık sık başarısız. Bir iç LAN tabanlı adresi etkin FTP belirtir, toowhich bir FTP sunucusu tooconnect büyük olasılıkla başarısız olur.
> 
> 

FTP kullanarak dağıtım tooan App Service web uygulaması hakkında daha fazla bilgi için aşağıdaki konularda hello bakın:

* [Bir FTP yardımcı programını kullanarak dağıtma](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a>Dağıtım kimlik bilgilerini ayarlayın
Merhaba çalıştırmak olduğundan emin olun **AzureWebDemo** uygulama toocreate bir web uygulaması. Dosyaları toothis konumu aktarır.

1. Oturum hello Klasik Portalı'na ve tıklatın **Web Apps**. Emin olun **WebDemoWebApp** hello web uygulamaları listesinde görüntülenir ve çalışır durumda olduğundan emin olun. Tıklatın **WebDemoWebApp** tooopen kendi **Pano** sayfası.
2. Merhaba üzerinde **Pano** sayfasında **Hızlı Bakış**, tıklatın **, dağıtım kimlik bilgilerini ayarlayın** (dağıtım kimlik bilgileri zaten varsa bu okur  **Dağıtım kimlik bilgilerinizi sıfırlayın**).
   
    Dağıtım kimlik bilgileri bir Microsoft hesabıyla ilişkilendirilmiş. Toospecify bir kullanıcı adı ve parola, Git ve FTP kullanarak toodeploy kullanabileceğiniz gerekir. Bu kimlik bilgileri toodeploy tooany web uygulaması, Microsoft hesabınızla ilişkili tüm Azure abonelikleri kullanabilirsiniz. Git ve FTP dağıtımı kimlik bilgilerini hello iletişim kutusunda, kayıt hello kullanıcı adı ve parola gelecekte kullanılmak üzere sağlayın.

#### <a name="get-ftp-connection-information"></a>FTP bağlantı bilgileri alma
toouse FTP toodeploy uygulama dosyaları toohello yeni oluşturulan web uygulaması, tooobtain bağlantı bilgilerini gerekir. Tooobtain bağlantı bilgilerini iki yolu vardır. Toovisit hello web uygulamanızın tek yönlü **Pano** sayfasında; hello diğer toodownload hello web uygulamanızın yayımlama profili yoludur. Merhaba yayımlama profili web uygulamalarınızda Azure App Service için FTP ana bilgisayar adı ve oturum açma kimlik bilgileri gibi bilgileri sağlayan bir XML dosyasıdır. Bu kullanıcı adı ve parola toodeploy tooany web uygulaması hello ile Azure hesabı değil yalnızca bu bir ilişkili tüm Aboneliklerde kullanabilirsiniz.

Merhaba web uygulamanızın dikey penceresinde hello tooobtain FTP bağlantı bilgileri [Azure Portal][Azure Portal]:

1. Altında **Essentials**, bulma ve kopyalama hello **FTP ana bilgisayar adı**. Bu çok benzer bir URI değil`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.
2. Altında **Essentials**, bulma ve kopyalama **FTP/dağıtım kullanıcı adı**. Bu hello biçimde olacaktır *webappname\deployment-username*; örneğin `WebDemoWebApp\deployer77`.

tooobtain FTP bağlantı bilgileri hello profili yayımlayın:

1. Merhaba web uygulamanızın dikey penceresinde tıklayın **Get yayımlama profili**. Bu .publishsettings dosyasını tooyour yerel bir sürücünün indirir.
2. Bir XML Düzenleyicisi'ni veya metin düzenleyicide hello .publishsettings dosyasını açın ve hello bulur `<publishProfile>` öğeyi içeren `publishMethod="FTP"`. Merhaba aşağıdaki gibi görünmelidir:
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. Bu hello web uygulamanızın Not `publishProfile` ayarları aşağıdaki gibi toohello FileZilla Site Yöneticisi ayarları eşleyin:

* `publishUrl`olduğundan, hello aynı **FTP konak adı**, hello içinde ayarladığınız değer **konak**.
* `publishMethod="FTP"`ayarladığınız anlamına gelir **Protokolü** çok**FTP - Dosya Aktarım Protokolü**, ve **şifreleme** çok**düz FTP Kullan**.
* `userName`ve `userPWD` hello tuşları belirtilen hello dağıtım kimlik bilgileri sıfırlandığında gerçek kullanıcı adı ve parola değerlerdir. `userName`olduğundan, hello aynı **dağıtım / FTP kullanıcısı**. Bunlar çok eşleme**kullanıcı** ve **parola** FileZilla içinde.
* `ftpPassiveMode="True"`Bu hello FTP sitesi edilgen FTP aktarımı kullanır anlamına gelir; seçin **pasif** hello üzerinde **aktarım ayarları** sekmesi.

#### <a name="configure-hello-web-app-toohost-a-java-application"></a>Merhaba Web uygulaması toohost bir Java uygulaması yapılandırma
Merhaba uygulaması yayımlamadan önce böylece hello web uygulaması bir Java uygulamasını barındırmak birkaç yapılandırma ayarlarını toochange gerekir.

1. Merhaba Klasik Portalı'nda, toohello web uygulamanızın Git **Pano** sayfasında ve tıklayın **yapılandırma**. Merhaba üzerinde **yapılandırma** sayfasında, ayarları aşağıdaki hello belirtin.
2. İçinde **Java sürümü** hello varsayılandır **devre dışı**; select hello Java sürümü, uygulama hedeflerine; örneğin 1.7.0_51. Bunu yaptıktan sonra da emin olmanız **Web kapsayıcısına** Tomcat sunucusunu tooa sürümünü ayarlayın.
3. İçinde **varsayılan belgeler**, index.jsp ekleyin ve toohello listenin hello taşır. (Merhaba varsayılan web uygulamaları için hostingstart.html dosyasıdır.)
4. **Kaydet** düğmesine tıklayın.

#### <a name="publish-your-application-using-kudu"></a>Kudu kullanarak uygulamanızı yayımlama
Tek yönlü toopublish hello toouse hello Kudu hata ayıklama Azure'da yerleşik konsol uygulamasıdır. Kudu toobe kararlı ve App Service Web Apps ve Tomcat Server ile tutarlı denir. Form aşağıdaki hello tooa URL'sini göz atarak hello konsol hello web uygulaması için erişim:

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. Bu yordam, hello Kudu konsol URL aşağıdaki hello bulunur; toothis konuma göz atın:
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. Merhaba üst menüsünden seçin **Hata Ayıkla Konsolu > CMD**.
3. Hello konsol komut satırında çok gidin`/site/wwwroot` (veya `site`, ardından `wwwroot` hello sayfanın üst kısmındaki hello hello dizin görünümünde):
   
    `cd /site/wwwroot`
4. Belirttikten sonra **Java Sürüm**, Tomcat sunucusunun webapps dizinine oluşturmanız. Merhaba konsol komut satırında toohello webapps dizinine gidin:
   
    `mkdir webapps`
   
    `cd webapps`
5. Gelen JSPHello.war sürükleyin `<project-path>/JSPHello/src/` ve gelsin hello Kudu dizini altında bırakma `/site/wwwroot/webapps`. Tomcat sıkıştırmasını çünkü bunu toohello "tooupload ve ZIP buraya sürükleyin" alanı, sürükleyin değil.
   
   ![][8]

İlk JSPHello.war hello dizin alanında kendisi tarafından görünür:

  ![][9]

Kısa bir süre (büyük olasılıkla 5 dakikadan daha az) paketten JSPHello dizine hello WAR dosyasını Tomcat sunucusunu ayıklayın. İndex.jsp olduğundan sıkıştırması açılmış ve orada kopyalanan olup olmadığını hello kök dizin toosee'ı tıklatın. Dizini oluşturulan JSPHello Hello açılmış olup olmadığını varsa, arka toohello webapps dizinine toosee gidin. Bu öğeleri görmüyorsanız bekleyin ve yineleyin.

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a>FileZilla (isteğe bağlı) kullanarak uygulamanızı yayımlama
Toopublish Merhaba uygulaması kullanabileceğiniz başka bir FileZilla, kolay ve grafik kullanıcı Arabirimi ile popüler bir üçüncü taraf FTP istemcisi aracıdır. Gelen FileZilla yükleyip [http://filezilla-project.org/](http://filezilla-project.org/) zaten olmayan. Hello hello istemci kullanma hakkında daha fazla bilgi için bkz: [FileZilla belgelerine](https://wiki.filezilla-project.org/Documentation) ve bu blog girişi [FTP istemcileri - bölümü 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).

1. FileZilla içinde tıklatın **Dosya > Site Yöneticisi**.
2. Merhaba, **Site Yöneticisi** iletişim kutusunda, tıklatın **Yeni Site**. Yeni ve boş bir FTP sitesi görünür **seçin girişi** tooprovide bir ad isteyen. Bu yordam, adlandırın `AzureWebDemo-FTP`.
   
    Merhaba üzerinde **genel** sekmesinde, ayarlar aşağıdaki hello belirtin:
   
   * **Ana bilgisayarı:** Enter hello **FTP konak adı** hello panodan kopyaladığınız.
   * **Bağlantı noktası:** (Bu bu pasif aktarımı ve hello sunucu başlangıç bağlantı noktası toouse belirleyecektir olarak boş bırakın.)
   * **Protokol:** FTP Dosya Aktarım Protokolü
   * **Şifreleme:** düz FTP Kullan
   * **Oturum açma türü:** Normal
   * **Kullanıcı:** Enter hello dağıtım / FTP kullanıcısı hello panodan kopyalanır. Merhaba form olan hello tam FTP kullanıcı adı, budur *webappname\username*.
   * **Parola:** hello dağıtım kimlik bilgileri ayarlandığında belirtilen hello parola gir.
     
     Merhaba üzerinde **aktarım ayarları** sekmesine **pasif**.
3. **Bağlan**'a tıklayın. Başarılı, FileZilla'nin Konsolu görüntüler varsa bir `Status: Connected` iletisi ve sorunu bir `LIST` toolist hello dizin içeriği komutu.
4. Merhaba, **yerel** site paneli seçin hello kaynak hangi hello JSPHello.war dosya dizindeki; hello yolu benzer toohello şu olacaktır:
   
    `<project-path>/JSPHello/src/`
5. Merhaba, **uzak** site paneli, select hello hedef klasör. Merhaba WAR dosyası toohello dağıtacağınız `webapps` hello web uygulamanızın kök altında dizin. Çok gidin`/site/wwwroot`, sağ tıklayın `wwwroot`seçip **dizin oluştur**. Adı hello dizini `webapps` ve o dizini girin.
6. JSPHello.war çok aktarım`/site/wwwroot/webapps`. Hello JSPHello.war seçin **yerel** dosya listesi, üzerinde sağ tıklatın ve seçin **karşıya**. Bunun görüntülendiğini görmeniz gerekir `/site/wwwroot/webapps`.
7. JSPHello.war toohello webapps dizinine kopyaladıktan sonra Tomcat sunucusunun otomatik olarak açın (sıkıştırmasını açın) hello hello WAR dosyasını dosyalarında. Tomcat sunucusunu hemen paketi açılırken başlasa uzun sürebilir hello FTP İstemcisi'nde hello dosyaları tooappear için süresi (büyük olasılıkla saat).

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a>Web uygulaması hello üzerinde Hello Hello World uygulamayı çalıştırın
1. Merhaba WAR dosyasını karşıya ve Tomcat sunucusunun bir paketten oluşturdu doğruladıktan sonra `JSPHello` dizini çok Gözat`http://webdemowebapp.azurewebsites.net/JSPHello` toorun Merhaba uygulaması.
   
   > **Not:** tıklatırsanız **Gözat** hello Klasik portalından hello varsayılan Web sayfası, "Bu temel Java web uygulaması başarıyla oluşturuldu." belirten alabilirsiniz Sipariş tooview hello uygulama çıktıda hello varsayılan Web sayfası yerine toorefresh hello Web sayfası olabilir.
   > 
   > 
2. Merhaba uygulamayı çalıştırdığında, çıktı aşağıdaki hello ile bir web sayfasını görmeniz gerekir:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a>Azure kaynakları temizlemek
Bu yordam, App Service web uygulaması oluşturur. Mevcut olduğu sürece hello kaynak için Fatura edilecek. Toocontinue hello web uygulaması sınama veya geliştirme için kullanmayı planlamıyorsanız, durdurma veya silme düşünmelisiniz. Durduruldu bir web uygulaması küçük bir ücret doğurur, ancak herhangi bir zamanda yeniden başlatabilirsiniz. Bir web uygulaması silme tooit karşıya yüklediğiniz tüm verileri siler.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
