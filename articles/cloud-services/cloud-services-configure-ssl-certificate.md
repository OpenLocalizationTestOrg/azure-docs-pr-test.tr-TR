---
title: "Bulut hizmeti (Klasik) için SSL aaaConfigure | Microsoft Docs"
description: "Bilgi nasıl toospecify web rolü nasıl tooupload bir SSL sertifikası ve toosecure uygulamanız için bir HTTPS uç nokta."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="c8e0f-103">Azure'da bir uygulama için SSL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c8e0f-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8e0f-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c8e0f-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="c8e0f-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="c8e0f-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="c8e0f-106">Güvenli Yuva Katmanı (SSL) şifreleme yöntemidir hello gönderilen veri korumanın en yaygın olarak kullanılan hello Internet.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-106">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="c8e0f-107">Bu ortak görev ele alınmaktadır nasıl toospecify web rolü nasıl tooupload bir SSL sertifikası ve toosecure uygulamanız için bir HTTPS uç nokta.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-107">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="c8e0f-108">Bu görevde Hello yordamlar tooAzure bulut Hizmetleri uygulanır; Uygulama hizmetleri için bkz: [bu](../app-service-web/web-sites-configure-ssl-certificate.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-108">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="c8e0f-109">Bu görev, bir üretim dağıtımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-109">This task uses a production deployment.</span></span> <span data-ttu-id="c8e0f-110">Hazırlama dağıtımı hakkında bilgi hello bu konunun sonunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-110">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="c8e0f-111">Okuma [bu](cloud-services-how-to-create-deploy.md) henüz bir bulut hizmeti oluşturmadıysanız, ilk makalesi.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="c8e0f-112">1. adım: bir SSL sertifikası alma</span><span class="sxs-lookup"><span data-stu-id="c8e0f-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="c8e0f-113">SSL tooconfigure bir uygulama için öncelikle tooget tarafından bir sertifika yetkilisi (CA) kullanan bu amaç için sertifikaları veren güvenilen bir üçüncü taraf imzalanmış bir SSL sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-113">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="c8e0f-114">Zaten bir yoksa, SSL sertifikaları sattığı bir şirketten tooobtain gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-114">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="c8e0f-115">Merhaba sertifika Azure SSL sertifikaları için gereksinimler aşağıdaki hello karşılaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="c8e0f-115">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="c8e0f-116">Merhaba sertifika özel anahtar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-116">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="c8e0f-117">anahtar değişimi için dışarı aktarılabilir tooa kişisel bilgi değişimi (.pfx) dosyasını Hello sertifika oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-117">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="c8e0f-118">Merhaba sertifikanın konu adı hello kullanılan etki alanı tooaccess hello bulut hizmeti eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-118">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="c8e0f-119">Merhaba cloudapp.net etki alanı için bir sertifika yetkilisinden (CA) bir SSL sertifikası elde edemiyor.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-119">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="c8e0f-120">Özel etki alanı adı toouse almalıdır hizmetinizi eriştiğinizde.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-120">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="c8e0f-121">Bir CA'dan bir sertifika isteme, hello sertifikanın konu adı, uygulamanızın hello özel etki alanı adı kullanılan tooaccess eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-121">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="c8e0f-122">Örneğin, özel etki alanı adınızı ise **contoso.com** CA'nız için bir sertifika istemesini ***. contoso.com** veya **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="c8e0f-123">Merhaba sertifika en az 2048 bit şifreleme kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-123">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="c8e0f-124">Test amaçları için yapabileceğiniz [oluşturma](cloud-services-certs-create.md) ve kendinden imzalı bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="c8e0f-125">Kendinden imzalı bir sertifika üzerinden bir CA kimliği doğrulanmamış ve hello cloudapp.net etki alanı hello Web sitesi URL'si kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-125">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="c8e0f-126">Örneğin, hello aşağıdaki görev hangi hello hello sertifikada kullanılan ortak ad (CN) olan otomatik olarak imzalanan bir sertifika kullanır **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-126">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="c8e0f-127">Ardından, hizmet yapılandırma dosyalarını ve hizmet tanımı içinde hello sertifikayla ilgili bilgileri içermelidir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-127">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="c8e0f-128">2. adım: hello Hizmet tanım ve yapılandırma dosyalarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="c8e0f-128">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="c8e0f-129">Uygulamanızı yapılandırılmış toouse hello sertifika olması gerekir ve bir HTTPS uç noktası eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-129">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="c8e0f-130">Sonuç olarak, hello hizmet tanımı ve hizmet yapılandırma dosyaları güncelleştirilmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-130">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="c8e0f-131">Geliştirme ortamınızı hello Hizmet tanım dosyası (CSDEF) açın, ekleme bir **sertifikaları** hello bölümde **WebRole** bölümünde ve bilgi aşağıdaki hello içerir sertifikası (ve Ara sertifikaları):</span><span class="sxs-lookup"><span data-stu-id="c8e0f-131">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>
   
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
   
   <span data-ttu-id="c8e0f-132">Merhaba **sertifikaları** bölümü hello adını bizim sertifika, konum ve hello deposunun bulunduğu olduğu hello adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-132">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>
   
   <span data-ttu-id="c8e0f-133">İzinler (`permisionLevel` özniteliği) olması kümesi tooone Merhaba, aşağıdaki değerleri:</span><span class="sxs-lookup"><span data-stu-id="c8e0f-133">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>
   
   | <span data-ttu-id="c8e0f-134">İzni değeri</span><span class="sxs-lookup"><span data-stu-id="c8e0f-134">Permission Value</span></span> | <span data-ttu-id="c8e0f-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8e0f-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="c8e0f-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="c8e0f-136">limitedOrElevated</span></span> |<span data-ttu-id="c8e0f-137">**(Varsayılan)**  Tüm rol işlemler hello özel anahtara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-137">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="c8e0f-138">yükseltilmiş</span><span class="sxs-lookup"><span data-stu-id="c8e0f-138">elevated</span></span> |<span data-ttu-id="c8e0f-139">Yalnızca yükseltilmiş işlemleri hello özel anahtara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-139">Only elevated processes can access hello private key.</span></span> |
2. <span data-ttu-id="c8e0f-140">Hizmet tanımı dosyasında eklemek bir **Inputendpoint** öğesi hello içinde **uç noktaları** tooenable HTTPS bölümü:</span><span class="sxs-lookup"><span data-stu-id="c8e0f-140">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>
   
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

3. <span data-ttu-id="c8e0f-141">Hizmet tanımı dosyasında eklemek bir **bağlama** öğesi hello içinde **siteleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-141">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="c8e0f-142">Bu bölümde bir HTTPS bağlama toomap uç nokta tooyour site ekler:</span><span class="sxs-lookup"><span data-stu-id="c8e0f-142">This section adds an HTTPS binding toomap the endpoint tooyour site:</span></span>
   
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
   
   <span data-ttu-id="c8e0f-143">Tüm hello gerekli değişiklikleri toohello hizmet tanımı dosyası tamamlandı ancak yine de tooadd hello sertifika bilgilerini hello hizmet yapılandırma dosyası gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-143">All hello required changes toohello service definition file have been completed, but you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="c8e0f-144">Hizmet yapılandırma dosyanızdaki (CSCFG) ServiceConfiguration.Cloud.cscfg, ekleme bir **sertifikaları** hello bölümde **rol** ile aşağıda gösterilen hello örnek parmak izi değerini değiştirerek bölümünde, Sertifikanızın:</span><span class="sxs-lookup"><span data-stu-id="c8e0f-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within hello **Role** section, replacing hello sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="c8e0f-145">(örnek kullanan önceki hello **sha1** hello parmak izi algoritması için.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-145">(hello preceding example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="c8e0f-146">Merhaba sertifikanızın parmak izi algoritması için uygun değeri belirtin.)</span><span class="sxs-lookup"><span data-stu-id="c8e0f-146">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="c8e0f-147">Güncelleştirilmiş Hello hizmet tanımı ve hizmet yapılandırma dosyalarını, dağıtımınızı tooAzure yükleme paketi.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-147">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="c8e0f-148">Kullanıyorsanız **cspack**, kullanmayan **/generateConfigurationFile** , eklediğiniz sertifika bilgilerini üzerine yazar olarak bayrak.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="c8e0f-149">3. adım: bir sertifikayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="c8e0f-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="c8e0f-150">Dağıtım paketi güncelleştirilmiş toouse hello sertifika bırakıldı ve bir HTTPS uç nokta eklenir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-150">Your deployment package has been updated toouse hello certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="c8e0f-151">Şimdi hello paketini ve sertifika tooAzure hello Klasik Azure portalı ile karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-151">Now you can upload hello package and certificate tooAzure with hello Azure classic portal.</span></span>

1. <span data-ttu-id="c8e0f-152">İçinde toohello oturum [Klasik Azure portalı][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="c8e0f-152">Log in toohello [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="c8e0f-153">Tıklatın **bulut Hizmetleri** hello sol taraftaki gezinti bölmesi.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-153">Click **Cloud Services** on hello left-side navigation pane.</span></span>
3. <span data-ttu-id="c8e0f-154">İstenen hello bulut hizmeti'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-154">Click hello desired cloud service.</span></span>
4. <span data-ttu-id="c8e0f-155">Merhaba tıklatın **sertifikaları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-155">Click hello **Certificates** tab.</span></span>
   
    ![Merhaba sertifikalar sekmesini tıklatın](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="c8e0f-157">Merhaba tıklatın **karşıya** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-157">Click hello **Upload** button.</span></span>
   
    ![Karşıya Yükle](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="c8e0f-159">Merhaba sağlamak **dosya**, **parola**, ardından **tam** (onay işareti hello).</span><span class="sxs-lookup"><span data-stu-id="c8e0f-159">Provide hello **File**, **Password**, then click **Complete** (hello checkmark).</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="c8e0f-160">4. adım: toohello rol HTTPS kullanarak bağlanın</span><span class="sxs-lookup"><span data-stu-id="c8e0f-160">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="c8e0f-161">Dağıtımınızı Azure'da da çalışır durumda, HTTPS kullanarak tooit bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-161">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="c8e0f-162">Buna Klasik Azure portalı Merhaba, dağıtımınızı seçin, ardından altında hello bağlantısına tıklayın **Site URL'si**.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-162">In hello Azure classic portal, select your deployment, then click hello link under **Site URL**.</span></span>
   
   ![Site URL'si belirleme][2]
2. <span data-ttu-id="c8e0f-164">Web tarayıcınızda hello bağlantı toouse değiştirme **https** yerine **http**ve başlangıç sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-164">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c8e0f-165">Merhaba otomatik olarak imzalanan sertifika ile ilişkili tooan HTTPS uç noktası göz attığınızda kendinden imzalı bir sertifika kullanıyorsanız, bir sertifika hatası hello tarayıcıda görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-165">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="c8e0f-166">Bir güvenilen sertifika yetkilisi tarafından imzalanmış bir sertifika kullanarak bu sorunları ortadan kaldırılır; Hello bu arada, hello hatayı yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-166">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="c8e0f-167">(Başka bir seçenek tooadd hello otomatik olarak imzalanan sertifika toohello kullanıcının güvenilen sertifika yetkilisi sertifika deposunda olur.)</span><span class="sxs-lookup"><span data-stu-id="c8e0f-167">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![SSL örnek web sitesi][3]

<span data-ttu-id="c8e0f-169">Hazırlama dağıtımı yerine Üretim dağıtımı için toouse SSL istiyorsanız, ilk dağıtım hazırlama hello için kullanılan toodetermine hello URL gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-169">If you want toouse SSL for a staging deployment instead of a production deployment, you first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="c8e0f-170">Bulut hizmeti toohello hazırlama ortamınızı bir sertifika veya sertifika bilgileri dahil etmeden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-170">Deploy your cloud service toohello staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="c8e0f-171">Uygulama dağıtıldıktan sonra hello Klasik Azure Portalı'nın listelendiğini hello GUID tabanlı URL belirleyebilirsiniz **Site URL'si** alan.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-171">Once deployed, you can determine hello GUID-based URL, which is listed in hello Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="c8e0f-172">Merhaba ortak adı (CN) eşit toohello GUID tabanlı URL ile bir sertifika oluşturun (örneğin, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="c8e0f-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="c8e0f-173">Bulut hizmeti kullanım hello Azure Klasik portalı tooadd hello sertifika tooyour hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-173">Use hello Azure classic portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="c8e0f-174">Ardından, CSDEF ve CSCFG hello sertifika bilgileri tooyour dosyaları ekleyin, uygulamanızın yeniden paketleyin ve aşamalı dağıtım toouse hello yeni paketinizi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c8e0f-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8e0f-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c8e0f-175">Next steps</span></span>
* <span data-ttu-id="c8e0f-176">[Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c8e0f-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="c8e0f-177">Nasıl çok öğrenin[bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c8e0f-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="c8e0f-178">Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="c8e0f-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="c8e0f-179">[Bulut hizmetinizi yönetme](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="c8e0f-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
