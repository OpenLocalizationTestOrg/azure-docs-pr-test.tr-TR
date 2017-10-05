---
title: "Bir bulut hizmeti (Klasik) için SSL yapılandırma | Microsoft Docs"
description: "Web rolü için bir HTTPS uç nokta belirtme ve uygulamanızın güvenliğini sağlamak için bir SSL sertifikasını nasıl yükleyeceğiniz öğrenin."
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
ms.openlocfilehash: edb9aaf6dae11c9b8a171b22bc8a17003f80d86b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="bd819-103">Azure'da bir uygulama için SSL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bd819-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd819-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="bd819-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="bd819-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="bd819-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="bd819-106">Güvenli Yuva Katmanı (SSL) şifrelemesi, İnternet üzerinden gönderilen verilerin güvenliğini sağlamak için en yaygın kullanılan yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="bd819-106">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="bd819-107">Bu yaygın görev bir web rolü için HTTPS uç noktasının nasıl belirtileceğini ve uygulamanızın güvenliğini sağlamak için SSL sertifikasının nasıl yükleneceğini ele alır.</span><span class="sxs-lookup"><span data-stu-id="bd819-107">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="bd819-108">Bu görevde yordamlar Azure bulut Hizmetleri için geçerlidir; Uygulama hizmetleri için bkz: [bu](../app-service-web/web-sites-configure-ssl-certificate.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="bd819-108">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="bd819-109">Bu görev, bir üretim dağıtımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="bd819-109">This task uses a production deployment.</span></span> <span data-ttu-id="bd819-110">Bu konunun sonunda hazırlama dağıtımı hakkında bilgi sağlanır.</span><span class="sxs-lookup"><span data-stu-id="bd819-110">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="bd819-111">Okuma [bu](cloud-services-how-to-create-deploy.md) henüz bir bulut hizmeti oluşturmadıysanız, ilk makalesi.</span><span class="sxs-lookup"><span data-stu-id="bd819-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="bd819-112">1. adım: bir SSL sertifikası alma</span><span class="sxs-lookup"><span data-stu-id="bd819-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="bd819-113">Bir uygulama için SSL yapılandırmak için önce bir sertifika yetkilisi (CA), kimin bu amaç için sertifikaları veren güvenilen bir üçüncü taraf imzalanmış bir SSL sertifikası almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd819-113">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="bd819-114">Zaten bir yoksa, bir SSL sertifikalarını sattığı bir şirketten edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd819-114">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="bd819-115">Sertifika Azure SSL sertifikaları için aşağıdaki gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="bd819-115">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="bd819-116">Sertifika bir özel anahtar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="bd819-116">The certificate must contain a private key.</span></span>
* <span data-ttu-id="bd819-117">Sertifikanın bir kişisel bilgi değişimi (.pfx) dosyasına dışarı aktarılabilir olarak, anahtar değişimi için oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd819-117">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="bd819-118">Sertifikanın konu adı, bulut hizmetine erişmek için kullanılan etki alanını eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd819-118">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="bd819-119">Cloudapp.net etki alanı için bir sertifika yetkilisinden (CA) bir SSL sertifikası elde edemiyor.</span><span class="sxs-lookup"><span data-stu-id="bd819-119">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="bd819-120">Kullanılacak özel etki alanı adı almalıdır hizmetinize erişmek.</span><span class="sxs-lookup"><span data-stu-id="bd819-120">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="bd819-121">Bir CA'dan bir sertifika isteme, sertifikanın konu adı, uygulamaya erişmek için kullanılan özel etki alanı adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="bd819-121">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="bd819-122">Örneğin, özel etki alanı adınızı ise **contoso.com** CA'nız için bir sertifika istemesini ***. contoso.com** veya **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="bd819-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="bd819-123">En az 2048 bit şifreleme sertifikası kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd819-123">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="bd819-124">Test amaçları için yapabileceğiniz [oluşturma](cloud-services-certs-create.md) ve kendinden imzalı bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd819-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="bd819-125">Kendinden imzalı bir sertifika üzerinden bir CA kimliği doğrulanmamış ve cloudapp.net etki alanı Web sitesi URL'si olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd819-125">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="bd819-126">Örneğin, aşağıdaki görev sertifikada kullanılan ortak ad (CN) olduğu otomatik olarak imzalanan bir sertifika kullanır **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="bd819-126">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="bd819-127">Ardından, sertifika hakkındaki bilgiler, hizmet tanımı ve hizmet yapılandırma dosyalarını eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd819-127">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="bd819-128">2. adım: Hizmet tanım ve yapılandırma dosyalarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="bd819-128">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="bd819-129">Uygulamanızı sertifikayı kullanmak üzere yapılandırılması gerekir ve bir HTTPS uç noktası eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="bd819-129">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="bd819-130">Sonuç olarak, hizmet yapılandırma dosyalarını ve hizmet tanımı güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd819-130">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="bd819-131">Geliştirme ortamınızı Hizmet tanım dosyası (CSDEF) açın, ekleme bir **sertifikaları** içinde bölümünde **WebRole** bölümünde ve sertifikası (ve Ara sertifikaları) hakkında aşağıdaki bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="bd819-131">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>
   
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
   
   <span data-ttu-id="bd819-132">**Sertifikaları** bölümü bizim sertifika, konumunu ve onu bulunduğu deposunun adını adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bd819-132">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>
   
   <span data-ttu-id="bd819-133">İzinler (`permisionLevel` özniteliği) aşağıdaki değerlerden birine ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="bd819-133">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>
   
   | <span data-ttu-id="bd819-134">İzni değeri</span><span class="sxs-lookup"><span data-stu-id="bd819-134">Permission Value</span></span> | <span data-ttu-id="bd819-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bd819-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="bd819-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="bd819-136">limitedOrElevated</span></span> |<span data-ttu-id="bd819-137">**(Varsayılan)**  Tüm rol işlemler özel anahtara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="bd819-137">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="bd819-138">yükseltilmiş</span><span class="sxs-lookup"><span data-stu-id="bd819-138">elevated</span></span> |<span data-ttu-id="bd819-139">Yükseltilmiş işlemleri yalnızca özel anahtara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="bd819-139">Only elevated processes can access the private key.</span></span> |
2. <span data-ttu-id="bd819-140">Hizmet tanımı dosyasında eklemek bir **Inputendpoint** öğesi içinde **uç noktaları** bölüm HTTPS'yi etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="bd819-140">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>
   
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

3. <span data-ttu-id="bd819-141">Hizmet tanımı dosyasında eklemek bir **bağlama** öğesi içinde **siteleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="bd819-141">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="bd819-142">Bu bölümde, sitenize uç noktaya eşlemek için bir HTTPS bağlaması ekler:</span><span class="sxs-lookup"><span data-stu-id="bd819-142">This section adds an HTTPS binding to map the endpoint to your site:</span></span>
   
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
   
   <span data-ttu-id="bd819-143">Hizmet tanımı dosyası için gerekli tüm değişiklikleri tamamlandı ancak hala service yapılandırma dosyasına sertifika bilgilerini eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd819-143">All the required changes to the service definition file have been completed, but you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="bd819-144">Hizmet yapılandırma dosyanızdaki (CSCFG) ServiceConfiguration.Cloud.cscfg, ekleme bir **sertifikaları** içinde bölümünde **rol** ile Aşağıda örnek parmak izi değerini değiştirerek bölümünde, sertifikanızı:</span><span class="sxs-lookup"><span data-stu-id="bd819-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within the **Role** section, replacing the sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="bd819-145">(Önceki örnekte kullanan **sha1** parmak izi algoritması için.</span><span class="sxs-lookup"><span data-stu-id="bd819-145">(The preceding example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="bd819-146">Sertifikanızın parmak izi algoritmanın uygun değeri belirtin.)</span><span class="sxs-lookup"><span data-stu-id="bd819-146">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="bd819-147">Hizmet tanımı ve hizmet yapılandırma dosyalarını güncelleştirildi, dağıtımınızı Azure'a yükleme paketi.</span><span class="sxs-lookup"><span data-stu-id="bd819-147">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="bd819-148">Kullanıyorsanız **cspack**, kullanmayan **/generateConfigurationFile** , eklediğiniz sertifika bilgilerini üzerine yazar olarak bayrak.</span><span class="sxs-lookup"><span data-stu-id="bd819-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="bd819-149">3. adım: bir sertifikayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="bd819-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="bd819-150">Dağıtım paketi sertifikayı kullanmak üzere güncelleştirilmiş ve bir HTTPS uç nokta eklenir.</span><span class="sxs-lookup"><span data-stu-id="bd819-150">Your deployment package has been updated to use the certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="bd819-151">Artık Azure Klasik portalı ile Azure için paket ve sertifika yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd819-151">Now you can upload the package and certificate to Azure with the Azure classic portal.</span></span>

1. <span data-ttu-id="bd819-152">Oturum [Klasik Azure portalı][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="bd819-152">Log in to the [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="bd819-153">Tıklatın **bulut Hizmetleri** sol taraftaki gezinti bölmesi.</span><span class="sxs-lookup"><span data-stu-id="bd819-153">Click **Cloud Services** on the left-side navigation pane.</span></span>
3. <span data-ttu-id="bd819-154">İstenen bulut hizmeti'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bd819-154">Click the desired cloud service.</span></span>
4. <span data-ttu-id="bd819-155">Tıklatın **sertifikaları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="bd819-155">Click the **Certificates** tab.</span></span>
   
    ![Sertifikalar sekmesini tıklatın](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="bd819-157">**Karşıya Yükle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd819-157">Click the **Upload** button.</span></span>
   
    ![Karşıya Yükle](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="bd819-159">Sağlamak **dosya**, **parola**, ardından **tam** (onay işaretine).</span><span class="sxs-lookup"><span data-stu-id="bd819-159">Provide the **File**, **Password**, then click **Complete** (the checkmark).</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="bd819-160">4. adım: rol HTTPS kullanarak bağlanın</span><span class="sxs-lookup"><span data-stu-id="bd819-160">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="bd819-161">Dağıtımınızı Azure'da da çalışır durumda, HTTPS kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="bd819-161">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="bd819-162">Azure Klasik portalında dağıtımınızı seçin, ardından altında bağlantıyı **Site URL'si**.</span><span class="sxs-lookup"><span data-stu-id="bd819-162">In the Azure classic portal, select your deployment, then click the link under **Site URL**.</span></span>
   
   ![Site URL'si belirleme][2]
2. <span data-ttu-id="bd819-164">Web tarayıcınızda kullanmak üzere bağlantıyı değiştirmek **https** yerine **http**ve sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="bd819-164">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bd819-165">Kendinden imzalı bir sertifikayla ilişkili bir HTTPS uç noktası için göz attığınızda kendinden imzalı bir sertifika kullanıyorsanız, bir sertifika hatası tarayıcıda görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd819-165">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="bd819-166">Bir güvenilen sertifika yetkilisi tarafından imzalanmış bir sertifika kullanarak bu sorunları ortadan kaldırılır; Bu arada, hatayı yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd819-166">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="bd819-167">(Başka bir kullanıcının güvenilen sertifika yetkilisi sertifika depolama alanına otomatik olarak imzalanan sertifika eklemek için bir seçenektir.)</span><span class="sxs-lookup"><span data-stu-id="bd819-167">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![SSL örnek web sitesi][3]

<span data-ttu-id="bd819-169">Hazırlama dağıtımı yerine Üretim dağıtımı için SSL kullanmak istiyorsanız, önce hazırlama dağıtımı için kullanılan URL belirlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd819-169">If you want to use SSL for a staging deployment instead of a production deployment, you first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="bd819-170">Bulut hizmeti, bir sertifika veya sertifika bilgileri dahil etmeden hazırlama ortamına dağıtın.</span><span class="sxs-lookup"><span data-stu-id="bd819-170">Deploy your cloud service to the staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="bd819-171">Uygulama dağıtıldıktan sonra Azure Klasik portalın içinde listelenen GUID tabanlı URL belirleyebilirsiniz **Site URL'si** alan.</span><span class="sxs-lookup"><span data-stu-id="bd819-171">Once deployed, you can determine the GUID-based URL, which is listed in the Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="bd819-172">Bir sertifika ortak adı (CN) GUID tabanlı URL eşit oluşturun (örneğin, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="bd819-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="bd819-173">Hazırlanan bulut hizmetinize sertifika eklemek için Klasik Azure portalını kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd819-173">Use the Azure classic portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="bd819-174">Ardından, sertifika bilgileri CSDEF ve CSCFG dosyalarınıza eklemek, uygulamanızın yeniden paketleyin ve yeni paketini kullanmak için hazırlanmış dağıtımınızı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bd819-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd819-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd819-175">Next steps</span></span>
* <span data-ttu-id="bd819-176">[Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bd819-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="bd819-177">Bilgi edinmek için nasıl [bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="bd819-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="bd819-178">Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="bd819-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="bd819-179">[Bulut hizmetinizi yönetme](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="bd819-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
