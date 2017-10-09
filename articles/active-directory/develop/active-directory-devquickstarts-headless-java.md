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
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a>Azure AD ile Java komut satırı uygulaması tooAccess bir API kullanma
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure AD Basit ve kolay toooutsource sağlar, web uygulamanızın Kimlik Yönetimi, tek oturum açma ve oturum kapatma yalnızca birkaç satır kod sağlama.  Java web uygulamaları, bunu topluluk odaklı ADAL4J hello Microsoft'un uygulaması kullanarak gerçekleştirebilirsiniz.

  ADAL4J için burada kullanacağız:

* Merhaba kullanıcı hello kimlik sağlayıcısı Azure AD kullanarak hello uygulamada oturum açın.
* Merhaba kullanıcı hakkındaki bazı bilgileri görüntüler.
* Oturum, kullanıcı hello uygulama dışında hello.

Toodo Bu sipariş, şunları yapmanız gerekir:

1. Bir uygulamayı Azure AD ile kaydetme
2. Uygulama toouse hello ADAL4J kitaplığınızın ayarlayın.
3. Merhaba ADAL4J kitaplığı tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD kullanın.
4. Merhaba kullanıcı hakkında veri çıkışı yazdırın.

başlatıldı, tooget [hello uygulama çatıyı indirmeniz](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) veya [tamamlandı hello örnek indirme](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).  Ayrıca, hangi tooregister Azure AD kiracısında uygulamanız gerekir.  Zaten yoksa, [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).

## <a name="1--register-an-application-with-azure-ad"></a>1.  Bir uygulamayı Azure AD ile kaydetme
tooenable, uygulama tooauthenticate kullanıcılarınızın kiracınızda ilk tooregister yeni bir uygulama gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Hesabınızda ve hello altında Hello üst çubuğunda tıklatın **Directory** listesinde, burada istediğiniz tooregister uygulamanızı hello Active Directory Kiracı seçin.
3. Tıklayın **daha Hizmetleri** sol taraftaki gezinti hello ve seçin **Azure Active Directory**.
4. Tıklayın **uygulama kayıtlar** ve **Ekle**.
5. Merhaba komut istemlerini izleyin ve yeni bir **Web uygulaması ve/veya Webapı**.
  * Merhaba **adı** Merhaba uygulama, uygulama tooend kullanıcılarınızın anlatmaktadır
  * Merhaba **oturum açma URL'si** , uygulamanızın hello temel URL'dir.  Merhaba çatıyı'nın varsayılan `http://localhost:8080/adal4jsample/`.
6. Kayıt tamamladıktan sonra AAD uygulamanızı benzersiz bir uygulama kimliği atar.  Bu değer gerekir hello sonraki bölümlerde, bu nedenle hello uygulama sekmesinden kopyalayın.
7. Merhaba gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si hello güncelleştirin. Merhaba **uygulama kimliği URI'si** uygulamanız için benzersiz bir tanımlayıcıdır.  Merhaba kuraldır toouse `https://<tenant-domain>/<app-name>`, örneğin `http://localhost:8080/adal4jsample/`.

Merhaba portalında uygulamanız için bir kez oluşturun. bir **anahtar** hello gelen **ayarları** sayfasında uygulamanız için ve aşağı kopyalayın.  Kısa süre sonra ihtiyacınız olacaktır.

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a>2. Uygulama toouse ADAL4J kitaplığı ve Maven kullanarak önkoşulları ayarlama
Burada, biz ADAL4J toouse hello Openıd Connect kimlik doğrulama protokolünü yapılandıracaksınız.  ADAL4J kullanılan tooissue oturum açma ve oturum kapatma isteklerini olması, hello kullanıcının oturumunu yönetmek ve başka şeyler arasında hello kullanıcı hakkında bilgi alın.

* Merhaba kök dizininde projenizin, açma/oluşturma `pom.xml` ve hello bulun `// TODO: provide dependencies for Maven` ve hello şununla değiştirin:

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



## <a name="3-create-hello-java-publicclient-file"></a>3. Merhaba Java PublicClient dosyası oluşturma
Yukarıda belirtildiği gibi biz hello kullanıcı olarak oturum açmış hello ilgili grafik API'si tooget verileri kullanacak. Bu toobe bize kolay için hem bir dosya toorepresent oluşturuyoruz bir **dizin nesnesi** ve tek tek dosya toorepresent hello **kullanıcı** böylece hello Java OO desenini kullanılabilir.

* Adlı bir dosya oluşturun `DirectoryObject.java` hangi toostore (düşündüğünüz ücretsiz toouse bu daha sonra diğer grafik yapmak için sorgu) DirectoryObject hakkındaki temel verileri kullanacağız. Kes/bu aşağıdan Yapıştır:

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


## <a name="compile-and-run-hello-sample"></a>Derleme ve hello örnek çalıştırma
Değiştirme geri tooyour kök dizini ve put birlikte kullanarak komut toobuild hello örnek aşağıdaki hello çalıştırın `maven`. Bu hello kullanacağı `pom.xml` bağımlılıkları için yazdığınız dosya.

`$ mvn package`

Şimdi olmalıdır bir `adal4jsample.war` dosyasını, `/targets` dizin. Tomcat kapsayıcısında dağıtan ve hello URL'yi ziyaret olabilir 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> Bu çok kolay toodeploy WAR hello son Tomcat sunucularıyla olur. Yalnızca çok gidin`http://localhost:8080/manager/` ve karşıya yükleme üzerinde hello yönergeleri izleyin, '' adal4jsample.war' dosyası. İçinde autodeploy sizin için hello doğru uç noktası.
> 
> 

## <a name="next-steps"></a>Sonraki Adımlar
Tebrikler! Artık çalışan bir hello özelliği tooauthenticate kullanıcılara Java uygulaması sahip, güvenli bir şekilde OAuth 2.0 kullanan Web API'leri çağırmak ve hello kullanıcı hakkındaki temel bilgileri alın.  Henüz yapmadıysanız, başlangıç saati toopopulate kiracınız bazı kullanıcılar ile sunulmuştur.

Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [burada bir .zip sağlanan](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), veya Github'dan kopyalayabilirsiniz:

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

