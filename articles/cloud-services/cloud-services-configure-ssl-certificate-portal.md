---
title: "Bir bulut hizmeti için SSL yapılandırma | Microsoft Docs"
description: "Web rolü için bir HTTPS uç nokta belirtme ve uygulamanızın güvenliğini sağlamak için bir SSL sertifikasını nasıl yükleyeceğiniz öğrenin. Bu örnekler Azure Portalı'nı kullanın."
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
ms.openlocfilehash: e5c8c3b098772c0586712305a577b24a6f0d924c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="8dbfd-104">Azure'da bir uygulama için SSL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8dbfd-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8dbfd-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="8dbfd-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="8dbfd-106">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="8dbfd-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="8dbfd-107">Güvenli Yuva Katmanı (SSL) şifrelemesi, İnternet üzerinden gönderilen verilerin güvenliğini sağlamak için en yaygın kullanılan yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-107">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="8dbfd-108">Bu yaygın görev bir web rolü için HTTPS uç noktasının nasıl belirtileceğini ve uygulamanızın güvenliğini sağlamak için SSL sertifikasının nasıl yükleneceğini ele alır.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-108">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="8dbfd-109">Bu görevde yordamlar Azure bulut Hizmetleri için geçerlidir; Uygulama hizmetleri için bkz: [bu](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="8dbfd-109">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="8dbfd-110">Bu görev, bir üretim dağıtımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-110">This task uses a production deployment.</span></span> <span data-ttu-id="8dbfd-111">Bu konunun sonunda hazırlama dağıtımı hakkında bilgi sağlanır.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-111">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="8dbfd-112">Okuma [bu](cloud-services-how-to-create-deploy-portal.md) henüz bir bulut hizmeti oluşturmadıysanız, ilk.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="8dbfd-113">1. adım: bir SSL sertifikası alma</span><span class="sxs-lookup"><span data-stu-id="8dbfd-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="8dbfd-114">Bir uygulama için SSL yapılandırmak için önce bir sertifika yetkilisi (CA), kimin bu amaç için sertifikaları veren güvenilen bir üçüncü taraf imzalanmış bir SSL sertifikası almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-114">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="8dbfd-115">Zaten bir yoksa, bir SSL sertifikalarını sattığı bir şirketten edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-115">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="8dbfd-116">Sertifika Azure SSL sertifikaları için aşağıdaki gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="8dbfd-116">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="8dbfd-117">Sertifika bir özel anahtar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-117">The certificate must contain a private key.</span></span>
* <span data-ttu-id="8dbfd-118">Sertifikanın bir kişisel bilgi değişimi (.pfx) dosyasına dışarı aktarılabilir olarak, anahtar değişimi için oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-118">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="8dbfd-119">Sertifikanın konu adı, bulut hizmetine erişmek için kullanılan etki alanını eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-119">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="8dbfd-120">Cloudapp.net etki alanı için bir sertifika yetkilisinden (CA) bir SSL sertifikası elde edemiyor.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-120">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="8dbfd-121">Kullanılacak özel etki alanı adı almalıdır hizmetinize erişmek.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-121">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="8dbfd-122">Bir CA'dan bir sertifika isteme, sertifikanın konu adı, uygulamaya erişmek için kullanılan özel etki alanı adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-122">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="8dbfd-123">Örneğin, özel etki alanı adınızı ise **contoso.com** CA'nız için bir sertifika istemesini ***. contoso.com** veya **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="8dbfd-124">En az 2048 bit şifreleme sertifikası kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-124">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="8dbfd-125">Test amaçları için yapabileceğiniz [oluşturma](cloud-services-certs-create.md) ve kendinden imzalı bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="8dbfd-126">Kendinden imzalı bir sertifika üzerinden bir CA kimliği doğrulanmamış ve cloudapp.net etki alanı Web sitesi URL'si olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-126">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="8dbfd-127">Örneğin, aşağıdaki görev sertifikada kullanılan ortak ad (CN) olduğu otomatik olarak imzalanan bir sertifika kullanır **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-127">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="8dbfd-128">Ardından, sertifika hakkındaki bilgiler, hizmet tanımı ve hizmet yapılandırma dosyalarını eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-128">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="8dbfd-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="8dbfd-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="8dbfd-130">2. adım: Hizmet tanım ve yapılandırma dosyalarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="8dbfd-130">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="8dbfd-131">Uygulamanızı sertifikayı kullanmak üzere yapılandırılması gerekir ve bir HTTPS uç noktası eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-131">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="8dbfd-132">Sonuç olarak, hizmet yapılandırma dosyalarını ve hizmet tanımı güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-132">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="8dbfd-133">Geliştirme ortamınızı Hizmet tanım dosyası (CSDEF) açın, ekleme bir **sertifikaları** içinde bölümünde **WebRole** bölümünde ve sertifikası (ve Ara sertifikaları) hakkında aşağıdaki bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="8dbfd-133">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by the CA root, you
            must include all the intermediate certificates
            here. You must list them here, even if they are
            not bound to any endpoints. Failing to list any of
            the intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   <span data-ttu-id="8dbfd-134">**Sertifikaları** bölümü bizim sertifika, konumunu ve onu bulunduğu deposunun adını adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-134">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>

   <span data-ttu-id="8dbfd-135">İzinler (`permisionLevel` özniteliği) aşağıdaki değerlerden birine ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="8dbfd-135">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>

   | <span data-ttu-id="8dbfd-136">İzni değeri</span><span class="sxs-lookup"><span data-stu-id="8dbfd-136">Permission Value</span></span> | <span data-ttu-id="8dbfd-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8dbfd-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="8dbfd-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="8dbfd-138">limitedOrElevated</span></span> |<span data-ttu-id="8dbfd-139">**(Varsayılan)**  Tüm rol işlemler özel anahtara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-139">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="8dbfd-140">yükseltilmiş</span><span class="sxs-lookup"><span data-stu-id="8dbfd-140">elevated</span></span> |<span data-ttu-id="8dbfd-141">Yükseltilmiş işlemleri yalnızca özel anahtara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-141">Only elevated processes can access the private key.</span></span> |

2. <span data-ttu-id="8dbfd-142">Hizmet tanımı dosyasında eklemek bir **Inputendpoint** öğesi içinde **uç noktaları** bölüm HTTPS'yi etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="8dbfd-142">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>

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

3. <span data-ttu-id="8dbfd-143">Hizmet tanımı dosyasında eklemek bir **bağlama** öğesi içinde **siteleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-143">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="8dbfd-144">Bu öğe, sitenize uç noktaya eşlemek için bir HTTPS bağlaması ekler:</span><span class="sxs-lookup"><span data-stu-id="8dbfd-144">This element adds an HTTPS binding to map the endpoint to your site:</span></span>

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

   <span data-ttu-id="8dbfd-145">Hizmet tanımı dosyası için gerekli tüm değişiklikleri tamamlandı; Ancak, yine sertifika bilgilerini service yapılandırma dosyasına eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-145">All the required changes to the service definition file have been completed; but, you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="8dbfd-146">Hizmet yapılandırma dosyanızdaki (CSCFG) ServiceConfiguration.Cloud.cscfg, ekleme bir **sertifikaları** , sertifikanızın değerle.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="8dbfd-147">Aşağıdaki kod örneği ayrıntılarını sunan **sertifikaları** bölümünde, parmak izi değeri dışında.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-147">The following code sample provides details of the **Certificates** section, except for the thumbprint value.</span></span>

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

<span data-ttu-id="8dbfd-148">(Bu örnekte **sha1** parmak izi algoritması için.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-148">(This example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="8dbfd-149">Sertifikanızın parmak izi algoritmanın uygun değeri belirtin.)</span><span class="sxs-lookup"><span data-stu-id="8dbfd-149">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="8dbfd-150">Hizmet tanımı ve hizmet yapılandırma dosyalarını güncelleştirildi, dağıtımınızı Azure'a yükleme paketi.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-150">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="8dbfd-151">Kullanıyorsanız **cspack**, kullanmayan **/generateConfigurationFile** yeni eklediğiniz sertifika bilgilerini üzerine yazar olarak bayrak.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="8dbfd-152">3. adım: bir sertifikayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="8dbfd-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="8dbfd-153">Azure Portalı'na bağlanmak ve...</span><span class="sxs-lookup"><span data-stu-id="8dbfd-153">Connect to the Azure portal and...</span></span>

1. <span data-ttu-id="8dbfd-154">İçinde **tüm kaynakları** bölüm portalında, bulut hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-154">In the **All resources** section of the Portal, select your cloud service.</span></span>

    ![Bulut hizmetinizi yayımlayın](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="8dbfd-156">Tıklatın **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-156">Click **Certificates**.</span></span>

    ![Sertifikaları simgesine tıklayın](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="8dbfd-158">Tıklatın **karşıya** sertifikaları alanının üstünde.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-158">Click **Upload** at the top of the certificates area.</span></span>

    ![Karşıya yükleme menü öğesini tıklatın](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="8dbfd-160">Sağlamak **dosya**, **parola**, ardından **karşıya** veri giriş alanı altındaki.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-160">Provide the **File**, **Password**, then click **Upload** at the bottom of the data entry area.</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="8dbfd-161">4. adım: rol HTTPS kullanarak bağlanın</span><span class="sxs-lookup"><span data-stu-id="8dbfd-161">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="8dbfd-162">Dağıtımınızı Azure'da da çalışır durumda, HTTPS kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-162">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="8dbfd-163">Tıklatın **Site URL'si** web tarayıcısını açın.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-163">Click the **Site URL** to open up the web browser.</span></span>

   ![Site URL'sini tıklatın](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="8dbfd-165">Web tarayıcınızda kullanmak üzere bağlantıyı değiştirmek **https** yerine **http**ve sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-165">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8dbfd-166">Kendinden imzalı bir sertifikayla ilişkili bir HTTPS uç noktası için göz attığınızda kendinden imzalı bir sertifika kullanıyorsanız, bir sertifika hatası tarayıcıda görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-166">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="8dbfd-167">Bir güvenilen sertifika yetkilisi tarafından imzalanmış bir sertifika kullanarak bu sorunları ortadan kaldırılır; Bu arada, hatayı yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-167">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="8dbfd-168">(Başka bir kullanıcının güvenilen sertifika yetkilisi sertifika depolama alanına otomatik olarak imzalanan sertifika eklemek için bir seçenektir.)</span><span class="sxs-lookup"><span data-stu-id="8dbfd-168">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Site Önizleme](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="8dbfd-170">Hazırlama dağıtımı yerine Üretim dağıtımı için SSL kullanmak istiyorsanız, önce hazırlama dağıtımı için kullanılan URL belirlemek gerekir.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-170">If you want to use SSL for a staging deployment instead of a production deployment, you'll first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="8dbfd-171">Bulut hizmetinizi dağıtıldıktan sonra hazırlık ortamı URL'si tarafından belirlenir **dağıtım kimliği** bu biçiminde GUID:`https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="8dbfd-171">Once your cloud service has been deployed, the URL to the staging environment is determined by the **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="8dbfd-172">Bir sertifika ortak adı (CN) GUID tabanlı URL eşit oluşturun (örneğin, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="8dbfd-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="8dbfd-173">Hazırlanan bulut hizmetinize sertifika eklemek için Portalı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-173">Use the portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="8dbfd-174">Ardından, sertifika bilgileri CSDEF ve CSCFG dosyalarınıza eklemek, uygulamanızın yeniden paketleyin ve yeni paketini kullanmak için hazırlanmış dağıtımınızı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8dbfd-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="8dbfd-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8dbfd-175">Next steps</span></span>
* <span data-ttu-id="8dbfd-176">[Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8dbfd-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="8dbfd-177">Bilgi edinmek için nasıl [bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8dbfd-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="8dbfd-178">Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8dbfd-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="8dbfd-179">[Bulut hizmetinizi yönetme](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8dbfd-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
