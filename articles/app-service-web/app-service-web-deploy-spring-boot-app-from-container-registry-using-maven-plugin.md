---
title: "Azure Web Apps toodeploy Azure kapsayıcı kayıt defteri tooAzure uygulama hizmeti yay önyükleme uygulamada aaaHow toouse Merhaba Maven eklentisi"
description: "Bu öğretici, ancak hello adımları toodeploy yay önyükleme uygulaması Azure kapsayıcı kayıt defteri tooAzure tooAzure uygulama hizmeti Maven eklentisi kullanarak yol gösterir."
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a><span data-ttu-id="54171-103">Nasıl toouse hello Maven eklentisi için Azure Web Apps toodeploy Azure kapsayıcı kayıt defteri tooAzure App Service içinde Spring önyükleme uygulama</span><span class="sxs-lookup"><span data-stu-id="54171-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app in Azure Container Registry tooAzure App Service</span></span>

<span data-ttu-id="54171-104">Merhaba  **[yay Framework]**  , Java geliştiricilerinin web, mobil ve API uygulamaları oluşturma yardımcı olan bir popüler açık kaynak çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="54171-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="54171-105">Bu öğretici kullanılarak oluşturulmuş bir örnek uygulama kullanır [yay önyükleme], kuralı güdümlü bir yaklaşım yay tooget kullanma çalışmaya hızla.</span><span class="sxs-lookup"><span data-stu-id="54171-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="54171-106">Bu makalede, nasıl toodeploy bir örnek yay önyükleme uygulama tooAzure kapsayıcı kayıt defteri ve ardından Maven eklentisi için Azure Web Apps toodeploy, uygulama tooAzure uygulama hizmeti hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="54171-106">This article demonstrates how toodeploy a sample Spring Boot application tooAzure Container Registry, and then use hello Maven Plugin for Azure Web Apps toodeploy your application tooAzure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="54171-107">Hello Azure Web uygulamaları için Maven eklentisi şu anda önizleme olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="54171-107">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="54171-108">Ek özellikler hello gelecek için planlanan olsa da, şimdilik yalnızca FTP Yayımlama, desteklenir.</span><span class="sxs-lookup"><span data-stu-id="54171-108">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="54171-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="54171-109">Prerequisites</span></span>

<span data-ttu-id="54171-110">Sipariş toocomplete hello adımlarda Bu öğreticide, Önkoşullar aşağıdaki toohave hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="54171-110">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="54171-111">Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].</span><span class="sxs-lookup"><span data-stu-id="54171-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="54171-112">Merhaba [Azure komut satırı arabirimi (CLI)].</span><span class="sxs-lookup"><span data-stu-id="54171-112">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="54171-113">Güncel [Java Geliştirme Seti (JDK)], 1,7 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="54171-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="54171-114">Apache'nın [Maven] aracını (sürüm 3) yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="54171-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="54171-115">A [Git] istemci.</span><span class="sxs-lookup"><span data-stu-id="54171-115">A [Git] client.</span></span>
* <span data-ttu-id="54171-116">A [Docker] istemci.</span><span class="sxs-lookup"><span data-stu-id="54171-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="54171-117">Toohello sanallaştırma gereksinimleri Bu öğreticinin bir sanal makinede bu makalede hello adımları izleyin olamaz; sanallaştırma özellikleri etkin bir fiziksel bilgisayar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="54171-117">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="54171-118">Docker web uygulaması üzerinde kopya hello örnek yay önyükleme</span><span class="sxs-lookup"><span data-stu-id="54171-118">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="54171-119">Bu bölümde kapsayıcılı yay önyükleme uygulama kopyalamak ve yerel olarak test.</span><span class="sxs-lookup"><span data-stu-id="54171-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="54171-120">Bir komut istemi veya terminal penceresi açın ve yerel dizin toohold yay önyükleme uygulama ve değişiklik toothat dizin oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="54171-120">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="54171-121">--ya da--</span><span class="sxs-lookup"><span data-stu-id="54171-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="54171-122">Kopya hello [Docker Başlarken yay önyüklemede] örnek proje hello dizinine oluşturduğunuz; örneğin:</span><span class="sxs-lookup"><span data-stu-id="54171-122">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="54171-123">Dizin tamamlandı toohello proje Değiştir; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="54171-123">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="54171-124">Maven kullanarak hello JAR dosyasını oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="54171-124">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="54171-125">Merhaba web uygulaması oluşturduğunuzda Maven kullanarak hello web uygulaması başlatın; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="54171-125">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="54171-126">Merhaba web uygulaması, bir web tarayıcısı kullanarak yerel olarak tooit göz atarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="54171-126">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="54171-127">Örneğin, hello curl kullanılabilir varsa, aşağıdaki komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="54171-127">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="54171-128">Görüntülenen iletiden hello görmeniz gerekir: **Docker Hello World**</span><span class="sxs-lookup"><span data-stu-id="54171-128">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Örnek uygulamayı yerel olarak göz atın][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="54171-130">Bir Azure hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="54171-130">Create an Azure service principal</span></span>

<span data-ttu-id="54171-131">Bu bölümde, Azure kapsayıcı tooAzure dağıtırken Maven eklentisi kullanır hello hizmet sorumlusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54171-131">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="54171-132">Bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="54171-132">Open a command prompt.</span></span>

1. <span data-ttu-id="54171-133">Azure CLI kullanarak Azure hesabınızda oturum hello:</span><span class="sxs-lookup"><span data-stu-id="54171-133">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="54171-134">Oturum açma Hello yönergeleri toocomplete hello süreci izleyin.</span><span class="sxs-lookup"><span data-stu-id="54171-134">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="54171-135">Bir Azure hizmet sorumlusu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="54171-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="54171-136">Burada `uuuuuuuu` hello kullanıcı adı ve `pppppppp` hello hizmet sorumlusu hello parolası.</span><span class="sxs-lookup"><span data-stu-id="54171-136">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="54171-137">Azure aşağıdaki örneğine hello benzer JSON ile yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="54171-137">Azure responds with JSON that resembles hello following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="54171-138">Kapsayıcı tooAzure hello Maven eklentisi toodeploy yapılandırdığınızda bu JSON yanıt hello değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="54171-138">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="54171-139">Merhaba `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, ve `tttttttt` olan yer tutucu değerlerini olduğunuz isteğe bağlı olarak bu örnek toomake daha kolay toomap kullanılan, Maven yapılandırdığınızda bu değerleri tootheir ilgili öğeleri `settings.xml` hello sonraki dosyayı bölüm.</span><span class="sxs-lookup"><span data-stu-id="54171-139">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="54171-140">Azure kapsayıcı hello Azure CLI kullanarak bir kayıt oluşturun</span><span class="sxs-lookup"><span data-stu-id="54171-140">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="54171-141">Bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="54171-141">Open a command prompt.</span></span>

1. <span data-ttu-id="54171-142">Azure hesabı tooyour oturum:</span><span class="sxs-lookup"><span data-stu-id="54171-142">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="54171-143">Hello için bir kaynak grubu, bu makaledeki kullanacağınız Azure kaynakları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="54171-143">Create a resource group for hello Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="54171-144">Değiştir `wingtiptoysresources` Bu örnekte, kaynak grubu için benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="54171-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="54171-145">Merhaba kaynak grubunda yay önyükleme uygulamanız için bir özel Azure kapsayıcı kayıt defteri oluşturun:</span><span class="sxs-lookup"><span data-stu-id="54171-145">Create a private Azure container registry in hello resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="54171-146">Değiştir `wingtiptoysregistry` Bu örnekte, kapsayıcı kayıt defteri için benzersiz bir ad ile.</span><span class="sxs-lookup"><span data-stu-id="54171-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="54171-147">Kapsayıcı kaydınız Hello parolasını Al:</span><span class="sxs-lookup"><span data-stu-id="54171-147">Retrieve hello password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="54171-148">Azure parolanızla yanıt verir; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="54171-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a><span data-ttu-id="54171-149">Azure kapsayıcı kayıt defteri ve Azure hizmet asıl tooyour Maven ayarları ekleme</span><span class="sxs-lookup"><span data-stu-id="54171-149">Add your Azure container registry and Azure service principal tooyour Maven settings</span></span>

1. <span data-ttu-id="54171-150">Maven açmak `settings.xml` dosyasını bir metin düzenleyicisinde; bu dosya yolunda hello örnekler aşağıdaki gibi olabilir:</span><span class="sxs-lookup"><span data-stu-id="54171-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="54171-151">Azure kapsayıcı kayıt defteri erişim ayarlarınız hello önceki Bu makale toohello bölümünden eklemek `<servers>` hello koleksiyonunda *settings.xml* dosya; örneğin:</span><span class="sxs-lookup"><span data-stu-id="54171-151">Add your Azure Container Registry access settings from hello previous section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="54171-152">Konumlar:</span><span class="sxs-lookup"><span data-stu-id="54171-152">Where:</span></span>
   <span data-ttu-id="54171-153">Öğesi</span><span class="sxs-lookup"><span data-stu-id="54171-153">Element</span></span> | <span data-ttu-id="54171-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="54171-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="54171-155">Özel Azure kapsayıcı kaydınız Hello adını içerir.</span><span class="sxs-lookup"><span data-stu-id="54171-155">Contains hello name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="54171-156">Özel Azure kapsayıcı kaydınız Hello adını içerir.</span><span class="sxs-lookup"><span data-stu-id="54171-156">Contains hello name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="54171-157">Bu makalenin hello önceki bölümde alınan hello parola içerir.</span><span class="sxs-lookup"><span data-stu-id="54171-157">Contains hello password you retrieved in hello previous section of this article.</span></span>

1. <span data-ttu-id="54171-158">Bu makale toohello önceki bir bölümünden Azure hizmet asıl ayarlarınızı ekleme `<servers>` hello koleksiyonunda *settings.xml* dosya; örneğin:</span><span class="sxs-lookup"><span data-stu-id="54171-158">Add your Azure service principal settings from an earlier section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="54171-159">Konumlar:</span><span class="sxs-lookup"><span data-stu-id="54171-159">Where:</span></span>
   <span data-ttu-id="54171-160">Öğesi</span><span class="sxs-lookup"><span data-stu-id="54171-160">Element</span></span> | <span data-ttu-id="54171-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="54171-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="54171-162">Web uygulaması tooAzure dağıttığınızda, Maven toolook, güvenlik ayarlarını kullanan benzersiz bir ad belirtir.</span><span class="sxs-lookup"><span data-stu-id="54171-162">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="54171-163">Merhaba içeren `appId` hizmet sorumlusu değeri.</span><span class="sxs-lookup"><span data-stu-id="54171-163">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="54171-164">Merhaba içeren `tenant` hizmet sorumlusu değeri.</span><span class="sxs-lookup"><span data-stu-id="54171-164">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="54171-165">Merhaba içeren `password` hizmet sorumlusu değeri.</span><span class="sxs-lookup"><span data-stu-id="54171-165">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="54171-166">Olan hello hedef Azure bulut ortamı tanımlar `AZURE` Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="54171-166">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="54171-167">(Tam bir listesi ortamlarının hello kullanılabilir [Azure Web uygulamaları için Maven eklentisi] belgeleri)</span><span class="sxs-lookup"><span data-stu-id="54171-167">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="54171-168">Kaydet ve Kapat hello *settings.xml* dosya.</span><span class="sxs-lookup"><span data-stu-id="54171-168">Save and close hello *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a><span data-ttu-id="54171-169">Docker kapsayıcısı yansıması oluştur ve tooyour Azure kapsayıcı kayıt defteri gönderme</span><span class="sxs-lookup"><span data-stu-id="54171-169">Build your Docker container image and push it tooyour Azure container registry</span></span>

1. <span data-ttu-id="54171-170">Yay önyükleme uygulamanız için tamamlandı toohello proje dizin (örneğin gidin "*C:\SpringBoot\gs-spring-boot-docker\complete*"veya"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") ve açık hello *pom.xml* ile dosya bir Metin Düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="54171-170">Navigate toohello completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="54171-171">Güncelleştirme hello `<properties>` hello koleksiyonunda *pom.xml* hello oturum açma sunucusu değeri bir dosyayla, Azure kapsayıcı kayıt defteri hello önceki bölümdeki Bu öğreticinin; örneğin:</span><span class="sxs-lookup"><span data-stu-id="54171-171">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="54171-172">Konumlar:</span><span class="sxs-lookup"><span data-stu-id="54171-172">Where:</span></span>
   <span data-ttu-id="54171-173">Öğesi</span><span class="sxs-lookup"><span data-stu-id="54171-173">Element</span></span> | <span data-ttu-id="54171-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="54171-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="54171-175">Özel Azure kapsayıcı kaydınız Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="54171-175">Specifies hello name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="54171-176">Ekleyerek türetilmiş özel Azure kapsayıcı kaydınız Hello URL'sini belirtir ". azurecr.io" özel kapsayıcı kaydınız toohello adı.</span><span class="sxs-lookup"><span data-stu-id="54171-176">Specifies hello URL of your private Azure container registry, which is derived by appending ".azurecr.io" toohello name of your private container registry.</span></span>

1. <span data-ttu-id="54171-177">Doğrulayın `<plugin>` hello Docker eklentisi için *pom.xml* dosyası Bu öğreticide hello oturum açma sunucusu adresi ve kayıt defteri adı hello önceki adımdaki hello doğru özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="54171-177">Verify that `<plugin>` for hello Docker plugin in your *pom.xml* file contains hello correct properties for hello login server address and registry name from hello previous step in this tutorial.</span></span> <span data-ttu-id="54171-178">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="54171-178">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="54171-179">Konumlar:</span><span class="sxs-lookup"><span data-stu-id="54171-179">Where:</span></span>
   <span data-ttu-id="54171-180">Öğesi</span><span class="sxs-lookup"><span data-stu-id="54171-180">Element</span></span> | <span data-ttu-id="54171-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="54171-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="54171-182">Özel Azure kapsayıcı kayıt defteri adını içeren hello özelliği belirtir.</span><span class="sxs-lookup"><span data-stu-id="54171-182">Specifies hello property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="54171-183">Özel Azure kapsayıcı kaydınız hello URL'sini içeren hello özelliği belirtir.</span><span class="sxs-lookup"><span data-stu-id="54171-183">Specifies hello property which contains hello URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="54171-184">Yay önyükleme uygulamanız için tamamlandı toohello proje dizinine gidin ve komut toorebuild Merhaba uygulaması aşağıdaki hello çalıştırın ve hello kapsayıcı tooyour Azure kapsayıcı kayıt defteri gönderme:</span><span class="sxs-lookup"><span data-stu-id="54171-184">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="54171-185">İsteğe bağlı: Gözat toohello [Azure portal] ve Docker kapsayıcısı görüntü adlı olduğundan emin olun **yay önyükleme docker gs** kapsayıcı kayıt defterinizde.</span><span class="sxs-lookup"><span data-stu-id="54171-185">OPTIONAL: Browse toohello [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Azure portalında kapsayıcı doğrulayın][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a><span data-ttu-id="54171-187">Pom.xml özelleştirme sonra derleme ve kapsayıcı tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="54171-187">Customize your pom.xml, then build and deploy your container tooAzure</span></span>

<span data-ttu-id="54171-188">Açık hello `pom.xml` dosyasını bir metin düzenleyicisinde yay önyükleme uygulamanız için ve hello bulun `<plugin>` öğesi için `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="54171-188">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="54171-189">Bu öğe aşağıdaki örneğine hello benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="54171-189">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="54171-190">Merhaba Maven eklentisi için değiştirebileceğiniz birkaç değer vardır ve bu öğelerin her biri için ayrıntılı bir açıklama hello kullanılabilir [Azure Web uygulamaları için Maven eklentisi] belgeleri.</span><span class="sxs-lookup"><span data-stu-id="54171-190">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="54171-191">Denirse, bu makaledeki vurgulama değer olan birkaç değerleri vardır:</span><span class="sxs-lookup"><span data-stu-id="54171-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="54171-192">Öğesi</span><span class="sxs-lookup"><span data-stu-id="54171-192">Element</span></span> | <span data-ttu-id="54171-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="54171-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="54171-194">Merhaba Hello sürümünü belirtir [Azure Web uygulamaları için Maven eklentisi].</span><span class="sxs-lookup"><span data-stu-id="54171-194">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="54171-195">Hello listelenen hello sürüm denetlemelisiniz [Maven merkezi depo](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) kullanmakta olduğunuz tooensure hello en son sürümü.</span><span class="sxs-lookup"><span data-stu-id="54171-195">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="54171-196">Merhaba kimlik doğrulama bilgilerini içeren bu örnekte Azure belirtir bir `<serverId>` içeren öğeyi `azure-auth`; Maven Maven içinde bu değer toolook hello Azure hizmet asıl değerleri kullanan *settings.xml* bu makalenin önceki bölümde tanımlanan dosya.</span><span class="sxs-lookup"><span data-stu-id="54171-196">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="54171-197">Olan hello hedef kaynak grubu belirtir `wingtiptoysresources` Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="54171-197">Specifies hello target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="54171-198">zaten yoksa, dağıtım sırasında hello kaynak grubu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="54171-198">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="54171-199">Web uygulamanız için Hello hedef adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="54171-199">Specifies hello target name for your web app.</span></span> <span data-ttu-id="54171-200">Bu örnekte hello hedef adıdır `maven-linux-app-${maven.build.timestamp}`, hello burada `${maven.build.timestamp}` soneki, bu örnek tooavoid çakışması eklenir.</span><span class="sxs-lookup"><span data-stu-id="54171-200">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="54171-201">(Merhaba zaman damgası isteğe bağlıdır; hello uygulama adı için benzersiz bir dize belirtin.)</span><span class="sxs-lookup"><span data-stu-id="54171-201">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="54171-202">Olan bu örnekte hello hedef bölgesi belirtir `westus`.</span><span class="sxs-lookup"><span data-stu-id="54171-202">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="54171-203">(Tam bir liste hello olan [Azure Web uygulamaları için Maven eklentisi] belgelerine.)</span><span class="sxs-lookup"><span data-stu-id="54171-203">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="54171-204">Merhaba adı ve URL, kapsayıcının içeren hello özellikleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="54171-204">Specifies hello properties which contain hello name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="54171-205">Web uygulaması tooAzure dağıtırken Maven toouse benzersiz ayarlarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="54171-205">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="54171-206">Bu örnekte, bir `<property>` öğesi içeren bir ad/değer çifti alt öğelerinin uygulamanızı hello bağlantı noktasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="54171-206">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="54171-207">Hello ayarları toochange hello bağlantı noktası numarasını bu örnekte yalnızca gerekli olan hello varsayılandan hello noktası değiştirilirken.</span><span class="sxs-lookup"><span data-stu-id="54171-207">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

1. <span data-ttu-id="54171-208">Merhaba komut istemi veya daha önce kullandığınız terminal penceresinden, tüm değişiklikleri toohello yaptıysanız Maven kullanarak hello JAR dosyasını yeniden *pom.xml* dosya; örneğin:</span><span class="sxs-lookup"><span data-stu-id="54171-208">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="54171-209">Web uygulaması tooAzure Maven kullanarak dağıtabilirsiniz; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="54171-209">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="54171-210">Maven web uygulama tooAzure dağıtacağınız; Merhaba web uygulaması zaten mevcut değilse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="54171-210">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="54171-211">Varsa hello belirten hello bölge `<region>` öğesi, *pom.xml* dağıtımınızı başlattığınızda dosya sunucuları yeterli yok, aşağıdaki örnek bir hata benzer toohello görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="54171-211">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="54171-212">Bu durumda, başka bir bölgeye ve yeniden çalıştırın, uygulamanızın Maven komutunu toodeploy hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54171-212">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="54171-213">Web dağıtıldığında mümkün toomanage olacaktır hello kullanarak [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="54171-213">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="54171-214">Web uygulamanızı listelenen **uygulama hizmetleri**:</span><span class="sxs-lookup"><span data-stu-id="54171-214">Your web app will be listed in **App Services**:</span></span>

   ![Azure portalında uygulama hizmetleri listelenen web uygulaması][AP01]

* <span data-ttu-id="54171-216">Ve web uygulamanızı hello listelenir URL hello **genel bakış** web uygulamanız için:</span><span class="sxs-lookup"><span data-stu-id="54171-216">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Web uygulamanız için Hello URL belirleme][AP02]

## <a name="next-steps"></a><span data-ttu-id="54171-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54171-218">Next steps</span></span>

<span data-ttu-id="54171-219">Bu makalede ele alınan çeşitli teknolojiler hello hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="54171-219">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="54171-220">[Azure Web uygulamaları için Maven eklentisi]</span><span class="sxs-lookup"><span data-stu-id="54171-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="54171-221">TooAzure hello Azure CLI gelen oturum</span><span class="sxs-lookup"><span data-stu-id="54171-221">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="54171-222">Bir Azure hizmet sorumlusu Azure CLI 2.0 ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54171-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="54171-223">Maven ayarları başvurusu</span><span class="sxs-lookup"><span data-stu-id="54171-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="54171-224">[Maven için docker eklentisi]</span><span class="sxs-lookup"><span data-stu-id="54171-224">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure komut satırı arabirimi (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Azure Web uygulamaları için Maven eklentisi]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Maven için docker eklentisi]: https://github.com/spotify/docker-maven-plugin
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[yay önyükleme]: http://projects.spring.io/spring-boot/
[Docker Başlarken yay önyüklemede]: https://github.com/spring-guides/gs-spring-boot-docker
[yay Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
