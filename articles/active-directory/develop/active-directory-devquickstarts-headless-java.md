---
title: "aaaAzure AD Java komut satırı Başlarken | Microsoft Docs"
description: "Nasıl toobuild bir Java tooaccess bir API kullanıcılar oturum açtığında satırı uygulaması komutu."
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 51e1a8f9-6ff0-4643-a350-0ba794e26fd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 9ba1d1e794928a39ca1f091bd0e6eba57ce3d6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a><span data-ttu-id="16856-103">Azure AD ile Java komut satırı uygulaması tooAccess bir API kullanma</span><span class="sxs-lookup"><span data-stu-id="16856-103">Using Java Command Line App tooAccess An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="16856-104">Azure AD Basit ve kolay toooutsource sağlar, web uygulamanızın Kimlik Yönetimi, tek oturum açma ve oturum kapatma yalnızca birkaç satır kod sağlama.</span><span class="sxs-lookup"><span data-stu-id="16856-104">Azure AD makes it simple and straightforward toooutsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="16856-105">Java web uygulamaları, bunu topluluk odaklı ADAL4J hello Microsoft'un uygulaması kullanarak gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16856-105">In Java web apps, you can accomplish this using Microsoft's implementation of hello community-driven ADAL4J.</span></span>

  <span data-ttu-id="16856-106">ADAL4J için burada kullanacağız:</span><span class="sxs-lookup"><span data-stu-id="16856-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="16856-107">Merhaba kullanıcı hello kimlik sağlayıcısı Azure AD kullanarak hello uygulamada oturum açın.</span><span class="sxs-lookup"><span data-stu-id="16856-107">Sign hello user into hello app using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="16856-108">Merhaba kullanıcı hakkındaki bazı bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="16856-108">Display some information about hello user.</span></span>
* <span data-ttu-id="16856-109">Oturum, kullanıcı hello uygulama dışında hello.</span><span class="sxs-lookup"><span data-stu-id="16856-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="16856-110">Toodo Bu sipariş, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="16856-110">In order toodo this, you'll need to:</span></span>

1. <span data-ttu-id="16856-111">Bir uygulamayı Azure AD ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="16856-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="16856-112">Uygulama toouse hello ADAL4J kitaplığınızın ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="16856-112">Set up your app toouse hello ADAL4J library.</span></span>
3. <span data-ttu-id="16856-113">Merhaba ADAL4J kitaplığı tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD kullanın.</span><span class="sxs-lookup"><span data-stu-id="16856-113">Use hello ADAL4J library tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="16856-114">Merhaba kullanıcı hakkında veri çıkışı yazdırın.</span><span class="sxs-lookup"><span data-stu-id="16856-114">Print out data about hello user.</span></span>

<span data-ttu-id="16856-115">başlatıldı, tooget [hello uygulama çatıyı indirmeniz](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) veya [tamamlandı hello örnek indirme](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="16856-115">tooget started, [download hello app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download hello completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="16856-116">Ayrıca, hangi tooregister Azure AD kiracısında uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="16856-116">You'll also need an Azure AD tenant in which tooregister your application.</span></span>  <span data-ttu-id="16856-117">Zaten yoksa, [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="16856-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="16856-118">1.  Bir uygulamayı Azure AD ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="16856-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="16856-119">tooenable, uygulama tooauthenticate kullanıcılarınızın kiracınızda ilk tooregister yeni bir uygulama gerekir.</span><span class="sxs-lookup"><span data-stu-id="16856-119">tooenable your app tooauthenticate users, you'll first need tooregister a new application in your tenant.</span></span>

1. <span data-ttu-id="16856-120">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16856-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="16856-121">Hesabınızda ve hello altında Hello üst çubuğunda tıklatın **Directory** listesinde, burada istediğiniz tooregister uygulamanızı hello Active Directory Kiracı seçin.</span><span class="sxs-lookup"><span data-stu-id="16856-121">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="16856-122">Tıklayın **daha Hizmetleri** sol taraftaki gezinti hello ve seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16856-122">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="16856-123">Tıklayın **uygulama kayıtlar** ve **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="16856-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="16856-124">Merhaba komut istemlerini izleyin ve yeni bir **Web uygulaması ve/veya Webapı**.</span><span class="sxs-lookup"><span data-stu-id="16856-124">Follow hello prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="16856-125">Merhaba **adı** Merhaba uygulama, uygulama tooend kullanıcılarınızın anlatmaktadır</span><span class="sxs-lookup"><span data-stu-id="16856-125">hello **name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="16856-126">Merhaba **oturum açma URL'si** , uygulamanızın hello temel URL'dir.</span><span class="sxs-lookup"><span data-stu-id="16856-126">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="16856-127">Merhaba çatıyı'nın varsayılan `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="16856-127">hello skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="16856-128">Kayıt tamamladıktan sonra AAD uygulamanızı benzersiz bir uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="16856-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="16856-129">Bu değer gerekir hello sonraki bölümlerde, bu nedenle hello uygulama sekmesinden kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="16856-129">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="16856-130">Merhaba gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si hello güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="16856-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="16856-131">Merhaba **uygulama kimliği URI'si** uygulamanız için benzersiz bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="16856-131">hello **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="16856-132">Merhaba kuraldır toouse `https://<tenant-domain>/<app-name>`, örneğin `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="16856-132">hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="16856-133">Merhaba portalında uygulamanız için bir kez oluşturun. bir **anahtar** hello gelen **ayarları** sayfasında uygulamanız için ve aşağı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="16856-133">Once in hello portal for your app create a **Key** from hello **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="16856-134">Kısa süre sonra ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="16856-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="16856-135">2. Uygulama toouse ADAL4J kitaplığı ve Maven kullanarak önkoşulları ayarlama</span><span class="sxs-lookup"><span data-stu-id="16856-135">2. Set up your app toouse ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="16856-136">Burada, biz ADAL4J toouse hello Openıd Connect kimlik doğrulama protokolünü yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="16856-136">Here, we'll configure ADAL4J toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="16856-137">ADAL4J kullanılan tooissue oturum açma ve oturum kapatma isteklerini olması, hello kullanıcının oturumunu yönetmek ve başka şeyler arasında hello kullanıcı hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="16856-137">ADAL4J will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

* <span data-ttu-id="16856-138">Merhaba kök dizininde projenizin, açma/oluşturma `pom.xml` ve hello bulun `// TODO: provide dependencies for Maven` ve hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="16856-138">In hello root directory of your project, open/create `pom.xml` and locate hello `// TODO: provide dependencies for Maven` and replace with hello following:</span></span>

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>public-client-adal4j-sample</artifactId>
    <packaging>jar</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>public-client-adal4j-sample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
</dependencies>
    <build>
        <finalName>public-client-adal4j-sample</finalName>
        <plugins>
                <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <mainClass>PublicClient</mainClass>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
      <plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <configuration>
    <archive>
      <manifest>
        <mainClass>PublicClient</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
        </plugins>
    </build>

</project>


```



## <a name="3-create-hello-java-publicclient-file"></a><span data-ttu-id="16856-139">3. Merhaba Java PublicClient dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="16856-139">3. Create hello Java PublicClient file</span></span>
<span data-ttu-id="16856-140">Yukarıda belirtildiği gibi biz hello kullanıcı olarak oturum açmış hello ilgili grafik API'si tooget verileri kullanacak.</span><span class="sxs-lookup"><span data-stu-id="16856-140">As indicated above, we will be using hello Graph API tooget data about hello logged in user.</span></span> <span data-ttu-id="16856-141">Bu toobe bize kolay için hem bir dosya toorepresent oluşturuyoruz bir **dizin nesnesi** ve tek tek dosya toorepresent hello **kullanıcı** böylece hello Java OO desenini kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="16856-141">For this toobe easy for us we should create both a file toorepresent a **Directory Object** and an individual file toorepresent hello **User** so that hello OO pattern of Java can be used.</span></span>

* <span data-ttu-id="16856-142">Adlı bir dosya oluşturun `DirectoryObject.java` hangi toostore (düşündüğünüz ücretsiz toouse bu daha sonra diğer grafik yapmak için sorgu) DirectoryObject hakkındaki temel verileri kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="16856-142">Create a file called `DirectoryObject.java` which we will use toostore basic data about any DirectoryObject (you can feel free toouse this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="16856-143">Kes/bu aşağıdan Yapıştır:</span><span class="sxs-lookup"><span data-stu-id="16856-143">You can cut/paste this from below:</span></span>

```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;

public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "2a4da06c-ff07-410d-af8a-542a512f5092";

    public static void main(String args[]) throws Exception {

        try (BufferedReader br = new BufferedReader(new InputStreamReader(
                System.in))) {
            System.out.print("Enter username: ");
            String username = br.readLine();
            System.out.print("Enter password: ");
            String password = br.readLine();

            AuthenticationResult result = getAccessTokenFromUserCredentials(
                    username, password);
            System.out.println("Access Token - " + result.getAccessToken());
            System.out.println("Refresh Token - " + result.getRefreshToken());
            System.out.println("ID Token - " + result.getIdToken());
        }
    }

    private static AuthenticationResult getAccessTokenFromUserCredentials(
            String username, String password) throws Exception {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(AUTHORITY, false, service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", CLIENT_ID, username, password,
                    null);
            result = future.get();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }
}


```


## <a name="compile-and-run-hello-sample"></a><span data-ttu-id="16856-144">Derleme ve hello örnek çalıştırma</span><span class="sxs-lookup"><span data-stu-id="16856-144">Compile and run hello sample</span></span>
<span data-ttu-id="16856-145">Değiştirme geri tooyour kök dizini ve put birlikte kullanarak komut toobuild hello örnek aşağıdaki hello çalıştırın `maven`.</span><span class="sxs-lookup"><span data-stu-id="16856-145">Change back out tooyour root directory and run hello following command toobuild hello sample you just put together using `maven`.</span></span> <span data-ttu-id="16856-146">Bu hello kullanacağı `pom.xml` bağımlılıkları için yazdığınız dosya.</span><span class="sxs-lookup"><span data-stu-id="16856-146">This will use hello `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="16856-147">Şimdi olmalıdır bir `adal4jsample.war` dosyasını, `/targets` dizin.</span><span class="sxs-lookup"><span data-stu-id="16856-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="16856-148">Tomcat kapsayıcısında dağıtan ve hello URL'yi ziyaret olabilir</span><span class="sxs-lookup"><span data-stu-id="16856-148">You may deploy that in your Tomcat container and visit hello URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="16856-149">Bu çok kolay toodeploy WAR hello son Tomcat sunucularıyla olur.</span><span class="sxs-lookup"><span data-stu-id="16856-149">It is very easy toodeploy a WAR with hello latest Tomcat servers.</span></span> <span data-ttu-id="16856-150">Yalnızca çok gidin`http://localhost:8080/manager/` ve karşıya yükleme üzerinde hello yönergeleri izleyin, '' adal4jsample.war' dosyası.</span><span class="sxs-lookup"><span data-stu-id="16856-150">Simply navigate too`http://localhost:8080/manager/` and follow hello instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="16856-151">İçinde autodeploy sizin için hello doğru uç noktası.</span><span class="sxs-lookup"><span data-stu-id="16856-151">It will autodeploy for you with hello correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="16856-152">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="16856-152">Next Steps</span></span>
<span data-ttu-id="16856-153">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="16856-153">Congratulations!</span></span> <span data-ttu-id="16856-154">Artık çalışan bir hello özelliği tooauthenticate kullanıcılara Java uygulaması sahip, güvenli bir şekilde OAuth 2.0 kullanan Web API'leri çağırmak ve hello kullanıcı hakkındaki temel bilgileri alın.</span><span class="sxs-lookup"><span data-stu-id="16856-154">You now have a working Java application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="16856-155">Henüz yapmadıysanız, başlangıç saati toopopulate kiracınız bazı kullanıcılar ile sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="16856-155">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>

<span data-ttu-id="16856-156">Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [burada bir .zip sağlanan](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), veya Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="16856-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

