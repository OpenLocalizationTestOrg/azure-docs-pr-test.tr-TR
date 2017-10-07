---
title: "bir bulut hizmeti için SSL aaaConfigure | Microsoft Docs"
description: "Bilgi nasıl toospecify web rolü nasıl tooupload bir SSL sertifikası ve toosecure uygulamanız için bir HTTPS uç nokta. Bu örnekler hello Azure portalını kullanın."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="5df6b-104">Azure'da bir uygulama için SSL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5df6b-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5df6b-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="5df6b-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="5df6b-106">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="5df6b-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="5df6b-107">Güvenli Yuva Katmanı (SSL) şifreleme yöntemidir hello gönderilen veri korumanın en yaygın olarak kullanılan hello Internet.</span><span class="sxs-lookup"><span data-stu-id="5df6b-107">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="5df6b-108">Bu ortak görev ele alınmaktadır nasıl toospecify web rolü nasıl tooupload bir SSL sertifikası ve toosecure uygulamanız için bir HTTPS uç nokta.</span><span class="sxs-lookup"><span data-stu-id="5df6b-108">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="5df6b-109">Bu görevde Hello yordamlar tooAzure bulut Hizmetleri uygulanır; Uygulama hizmetleri için bkz: [bu](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="5df6b-109">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="5df6b-110">Bu görev, bir üretim dağıtımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="5df6b-110">This task uses a production deployment.</span></span> <span data-ttu-id="5df6b-111">Hazırlama dağıtımı hakkında bilgi hello bu konunun sonunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5df6b-111">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="5df6b-112">Okuma [bu](cloud-services-how-to-create-deploy-portal.md) henüz bir bulut hizmeti oluşturmadıysanız, ilk.</span><span class="sxs-lookup"><span data-stu-id="5df6b-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="5df6b-113">1. adım: bir SSL sertifikası alma</span><span class="sxs-lookup"><span data-stu-id="5df6b-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="5df6b-114">SSL tooconfigure bir uygulama için öncelikle tooget tarafından bir sertifika yetkilisi (CA) kullanan bu amaç için sertifikaları veren güvenilen bir üçüncü taraf imzalanmış bir SSL sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-114">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="5df6b-115">Zaten bir yoksa, SSL sertifikaları sattığı bir şirketten tooobtain gerekir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-115">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="5df6b-116">Merhaba sertifika Azure SSL sertifikaları için gereksinimler aşağıdaki hello karşılaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="5df6b-116">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="5df6b-117">Merhaba sertifika özel anahtar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-117">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="5df6b-118">anahtar değişimi için dışarı aktarılabilir tooa kişisel bilgi değişimi (.pfx) dosyasını Hello sertifika oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-118">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="5df6b-119">Merhaba sertifikanın konu adı hello kullanılan etki alanı tooaccess hello bulut hizmeti eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-119">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="5df6b-120">Merhaba cloudapp.net etki alanı için bir sertifika yetkilisinden (CA) bir SSL sertifikası elde edemiyor.</span><span class="sxs-lookup"><span data-stu-id="5df6b-120">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="5df6b-121">Özel etki alanı adı toouse almalıdır hizmetinizi eriştiğinizde.</span><span class="sxs-lookup"><span data-stu-id="5df6b-121">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="5df6b-122">Bir CA'dan bir sertifika isteme, hello sertifikanın konu adı, uygulamanızın hello özel etki alanı adı kullanılan tooaccess eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-122">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="5df6b-123">Örneğin, özel etki alanı adınızı ise **contoso.com** CA'nız için bir sertifika istemesini ***. contoso.com** veya **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="5df6b-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="5df6b-124">Merhaba sertifika en az 2048 bit şifreleme kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-124">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="5df6b-125">Test amaçları için yapabileceğiniz [oluşturma](cloud-services-certs-create.md) ve kendinden imzalı bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="5df6b-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="5df6b-126">Kendinden imzalı bir sertifika üzerinden bir CA kimliği doğrulanmamış ve hello cloudapp.net etki alanı hello Web sitesi URL'si kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5df6b-126">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="5df6b-127">Örneğin, hello aşağıdaki görev hangi hello hello sertifikada kullanılan ortak ad (CN) olan otomatik olarak imzalanan bir sertifika kullanır **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="5df6b-127">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="5df6b-128">Ardından, hizmet yapılandırma dosyalarını ve hizmet tanımı içinde hello sertifikayla ilgili bilgileri içermelidir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-128">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="5df6b-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="5df6b-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="5df6b-130">2. adım: hello Hizmet tanım ve yapılandırma dosyalarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="5df6b-130">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="5df6b-131">Uygulamanızı yapılandırılmış toouse hello sertifika olması gerekir ve bir HTTPS uç noktası eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-131">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="5df6b-132">Sonuç olarak, hello hizmet tanımı ve hizmet yapılandırma dosyaları güncelleştirilmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-132">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="5df6b-133">Geliştirme ortamınızı hello Hizmet tanım dosyası (CSDEF) açın, ekleme bir **sertifikaları** hello bölümde **WebRole** bölümünde ve bilgi aşağıdaki hello içerir sertifikası (ve Ara sertifikaları):</span><span class="sxs-lookup"><span data-stu-id="5df6b-133">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   <span data-ttu-id="5df6b-134">Merhaba **sertifikaları** bölümü hello adını bizim sertifika, konum ve hello deposunun bulunduğu olduğu hello adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5df6b-134">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>

   <span data-ttu-id="5df6b-135">İzinler (`permisionLevel` özniteliği) olması kümesi tooone Merhaba, aşağıdaki değerleri:</span><span class="sxs-lookup"><span data-stu-id="5df6b-135">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>

   | <span data-ttu-id="5df6b-136">İzni değeri</span><span class="sxs-lookup"><span data-stu-id="5df6b-136">Permission Value</span></span> | <span data-ttu-id="5df6b-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5df6b-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="5df6b-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="5df6b-138">limitedOrElevated</span></span> |<span data-ttu-id="5df6b-139">**(Varsayılan)**  Tüm rol işlemler hello özel anahtara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-139">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="5df6b-140">yükseltilmiş</span><span class="sxs-lookup"><span data-stu-id="5df6b-140">elevated</span></span> |<span data-ttu-id="5df6b-141">Yalnızca yükseltilmiş işlemleri hello özel anahtara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-141">Only elevated processes can access hello private key.</span></span> |

2. <span data-ttu-id="5df6b-142">Hizmet tanımı dosyasında eklemek bir **Inputendpoint** öğesi hello içinde **uç noktaları** tooenable HTTPS bölümü:</span><span class="sxs-lookup"><span data-stu-id="5df6b-142">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. <span data-ttu-id="5df6b-143">Hizmet tanımı dosyasında eklemek bir **bağlama** öğesi hello içinde **siteleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="5df6b-143">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="5df6b-144">Bu öğe bir HTTPS bağlama toomap uç nokta tooyour site ekler:</span><span class="sxs-lookup"><span data-stu-id="5df6b-144">This element adds an HTTPS binding toomap the endpoint tooyour site:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   <span data-ttu-id="5df6b-145">Tüm hello gerekli değişiklikleri toohello hizmet tanımı dosyası tamamlandı; Ancak, yine de tooadd hello sertifika bilgilerini hello hizmet yapılandırma dosyası gerekir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-145">All hello required changes toohello service definition file have been completed; but, you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="5df6b-146">Hizmet yapılandırma dosyanızdaki (CSCFG) ServiceConfiguration.Cloud.cscfg, ekleme bir **sertifikaları** , sertifikanızın değerle.</span><span class="sxs-lookup"><span data-stu-id="5df6b-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="5df6b-147">Merhaba aşağıdaki kod örneği ayrıntılarını hello sunan **sertifikaları** hello parmak izi değeri dışında bölümü.</span><span class="sxs-lookup"><span data-stu-id="5df6b-147">hello following code sample provides details of hello **Certificates** section, except for hello thumbprint value.</span></span>

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

<span data-ttu-id="5df6b-148">(Bu örnekte **sha1** hello parmak izi algoritması için.</span><span class="sxs-lookup"><span data-stu-id="5df6b-148">(This example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="5df6b-149">Merhaba sertifikanızın parmak izi algoritması için uygun değeri belirtin.)</span><span class="sxs-lookup"><span data-stu-id="5df6b-149">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="5df6b-150">Güncelleştirilmiş Hello hizmet tanımı ve hizmet yapılandırma dosyalarını, dağıtımınızı tooAzure yükleme paketi.</span><span class="sxs-lookup"><span data-stu-id="5df6b-150">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="5df6b-151">Kullanıyorsanız **cspack**, kullanmayan **/generateConfigurationFile** yeni eklediğiniz sertifika bilgilerini üzerine yazar olarak bayrak.</span><span class="sxs-lookup"><span data-stu-id="5df6b-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="5df6b-152">3. adım: bir sertifikayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="5df6b-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="5df6b-153">Toohello Azure portalına bağlanmak ve...</span><span class="sxs-lookup"><span data-stu-id="5df6b-153">Connect toohello Azure portal and...</span></span>

1. <span data-ttu-id="5df6b-154">Merhaba, **tüm kaynakları** hello portalı bölümünde, bulut hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="5df6b-154">In hello **All resources** section of hello Portal, select your cloud service.</span></span>

    ![Bulut hizmetinizi yayımlayın](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="5df6b-156">Tıklatın **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="5df6b-156">Click **Certificates**.</span></span>

    ![Merhaba sertifikaları simgesine tıklayın](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="5df6b-158">Tıklatın **karşıya** hello sertifikaları alanının hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="5df6b-158">Click **Upload** at hello top of hello certificates area.</span></span>

    ![Merhaba karşıya yükleme menü öğesini tıklatın](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="5df6b-160">Hello sağlamak **dosya**, **parola**, ardından **karşıya** hello altındaki hello veri giriş alanı.</span><span class="sxs-lookup"><span data-stu-id="5df6b-160">Provide hello **File**, **Password**, then click **Upload** at hello bottom of hello data entry area.</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="5df6b-161">4. adım: toohello rol HTTPS kullanarak bağlanın</span><span class="sxs-lookup"><span data-stu-id="5df6b-161">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="5df6b-162">Dağıtımınızı Azure'da da çalışır durumda, HTTPS kullanarak tooit bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-162">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="5df6b-163">Merhaba tıklatın **Site URL'si** tooopen hello web tarayıcısı ayarlama.</span><span class="sxs-lookup"><span data-stu-id="5df6b-163">Click hello **Site URL** tooopen up hello web browser.</span></span>

   ![Merhaba Site URL'Sİ'ı tıklatın](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="5df6b-165">Web tarayıcınızda hello bağlantı toouse değiştirme **https** yerine **http**ve başlangıç sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="5df6b-165">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5df6b-166">Merhaba otomatik olarak imzalanan sertifika ile ilişkili tooan HTTPS uç noktası göz attığınızda kendinden imzalı bir sertifika kullanıyorsanız, bir sertifika hatası hello tarayıcıda görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5df6b-166">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="5df6b-167">Bir güvenilen sertifika yetkilisi tarafından imzalanmış bir sertifika kullanarak bu sorunları ortadan kaldırılır; Hello bu arada, hello hatayı yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5df6b-167">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="5df6b-168">(Başka bir seçenek tooadd hello otomatik olarak imzalanan sertifika toohello kullanıcının güvenilen sertifika yetkilisi sertifika deposunda olur.)</span><span class="sxs-lookup"><span data-stu-id="5df6b-168">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Site Önizleme](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="5df6b-170">Hazırlama dağıtımı yerine Üretim dağıtımı için toouse SSL istiyorsanız, önce dağıtım hazırlama hello için kullanılan toodetermine hello URL gerekir.</span><span class="sxs-lookup"><span data-stu-id="5df6b-170">If you want toouse SSL for a staging deployment instead of a production deployment, you'll first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="5df6b-171">Bulut hizmetinizi dağıtıldıktan sonra ortam hazırlama hello URL toohello hello tarafından belirlenir **dağıtım kimliği** bu biçiminde GUID:`https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="5df6b-171">Once your cloud service has been deployed, hello URL toohello staging environment is determined by hello **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="5df6b-172">Merhaba ortak adı (CN) eşit toohello GUID tabanlı URL ile bir sertifika oluşturun (örneğin, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="5df6b-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="5df6b-173">Bulut hizmeti kullanım hello portal tooadd hello sertifika tooyour hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="5df6b-173">Use hello portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="5df6b-174">Ardından, CSDEF ve CSCFG hello sertifika bilgileri tooyour dosyaları ekleyin, uygulamanızın yeniden paketleyin ve aşamalı dağıtım toouse hello yeni paketinizi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5df6b-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="5df6b-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5df6b-175">Next steps</span></span>
* <span data-ttu-id="5df6b-176">[Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5df6b-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="5df6b-177">Nasıl çok öğrenin[bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5df6b-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="5df6b-178">Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5df6b-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="5df6b-179">[Bulut hizmetinizi yönetme](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5df6b-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
