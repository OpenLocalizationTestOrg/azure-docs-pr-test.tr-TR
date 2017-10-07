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
# <a name="configuring-ssl-for-an-application-in-azure"></a>Azure'da bir uygulama için SSL yapılandırma
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-configure-ssl-certificate-portal.md)
> * [Klasik Azure Portalı](cloud-services-configure-ssl-certificate.md)
> 
> 

Güvenli Yuva Katmanı (SSL) şifreleme yöntemidir hello gönderilen veri korumanın en yaygın olarak kullanılan hello Internet. Bu ortak görev ele alınmaktadır nasıl toospecify web rolü nasıl tooupload bir SSL sertifikası ve toosecure uygulamanız için bir HTTPS uç nokta.

> [!NOTE]
> Bu görevde Hello yordamlar tooAzure bulut Hizmetleri uygulanır; Uygulama hizmetleri için bkz: [bu](../app-service-web/web-sites-configure-ssl-certificate.md) makalesi.
> 
> 

Bu görev, bir üretim dağıtımı kullanır. Hazırlama dağıtımı hakkında bilgi hello bu konunun sonunda sağlanır.

Okuma [bu](cloud-services-how-to-create-deploy.md) henüz bir bulut hizmeti oluşturmadıysanız, ilk makalesi.

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a>1. adım: bir SSL sertifikası alma
SSL tooconfigure bir uygulama için öncelikle tooget tarafından bir sertifika yetkilisi (CA) kullanan bu amaç için sertifikaları veren güvenilen bir üçüncü taraf imzalanmış bir SSL sertifikası gerekir. Zaten bir yoksa, SSL sertifikaları sattığı bir şirketten tooobtain gerekir.

Merhaba sertifika Azure SSL sertifikaları için gereksinimler aşağıdaki hello karşılaması gerekir:

* Merhaba sertifika özel anahtar içermelidir.
* anahtar değişimi için dışarı aktarılabilir tooa kişisel bilgi değişimi (.pfx) dosyasını Hello sertifika oluşturulması gerekir.
* Merhaba sertifikanın konu adı hello kullanılan etki alanı tooaccess hello bulut hizmeti eşleşmelidir. Merhaba cloudapp.net etki alanı için bir sertifika yetkilisinden (CA) bir SSL sertifikası elde edemiyor. Özel etki alanı adı toouse almalıdır hizmetinizi eriştiğinizde. Bir CA'dan bir sertifika isteme, hello sertifikanın konu adı, uygulamanızın hello özel etki alanı adı kullanılan tooaccess eşleşmesi gerekir. Örneğin, özel etki alanı adınızı ise **contoso.com** CA'nız için bir sertifika istemesini ***. contoso.com** veya **www.contoso.com**.
* Merhaba sertifika en az 2048 bit şifreleme kullanmanız gerekir.

Test amaçları için yapabileceğiniz [oluşturma](cloud-services-certs-create.md) ve kendinden imzalı bir sertifika kullanın. Kendinden imzalı bir sertifika üzerinden bir CA kimliği doğrulanmamış ve hello cloudapp.net etki alanı hello Web sitesi URL'si kullanabilirsiniz. Örneğin, hello aşağıdaki görev hangi hello hello sertifikada kullanılan ortak ad (CN) olan otomatik olarak imzalanan bir sertifika kullanır **sslexample.cloudapp.net**.

Ardından, hizmet yapılandırma dosyalarını ve hizmet tanımı içinde hello sertifikayla ilgili bilgileri içermelidir.

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a>2. adım: hello Hizmet tanım ve yapılandırma dosyalarını değiştirme
Uygulamanızı yapılandırılmış toouse hello sertifika olması gerekir ve bir HTTPS uç noktası eklenmelidir. Sonuç olarak, hello hizmet tanımı ve hizmet yapılandırma dosyaları güncelleştirilmiş toobe gerekir.

1. Geliştirme ortamınızı hello Hizmet tanım dosyası (CSDEF) açın, ekleme bir **sertifikaları** hello bölümde **WebRole** bölümünde ve bilgi aşağıdaki hello içerir sertifikası (ve Ara sertifikaları):
   
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
   
   Merhaba **sertifikaları** bölümü hello adını bizim sertifika, konum ve hello deposunun bulunduğu olduğu hello adını tanımlar.
   
   İzinler (`permisionLevel` özniteliği) olması kümesi tooone Merhaba, aşağıdaki değerleri:
   
   | İzni değeri | Açıklama |
   | --- | --- |
   | limitedOrElevated |**(Varsayılan)**  Tüm rol işlemler hello özel anahtara erişebilir. |
   | yükseltilmiş |Yalnızca yükseltilmiş işlemleri hello özel anahtara erişebilir. |
2. Hizmet tanımı dosyasında eklemek bir **Inputendpoint** öğesi hello içinde **uç noktaları** tooenable HTTPS bölümü:
   
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

3. Hizmet tanımı dosyasında eklemek bir **bağlama** öğesi hello içinde **siteleri** bölümü. Bu bölümde bir HTTPS bağlama toomap uç nokta tooyour site ekler:
   
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
   
   Tüm hello gerekli değişiklikleri toohello hizmet tanımı dosyası tamamlandı ancak yine de tooadd hello sertifika bilgilerini hello hizmet yapılandırma dosyası gerekir.
4. Hizmet yapılandırma dosyanızdaki (CSCFG) ServiceConfiguration.Cloud.cscfg, ekleme bir **sertifikaları** hello bölümde **rol** ile aşağıda gösterilen hello örnek parmak izi değerini değiştirerek bölümünde, Sertifikanızın:
   
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

(örnek kullanan önceki hello **sha1** hello parmak izi algoritması için. Merhaba sertifikanızın parmak izi algoritması için uygun değeri belirtin.)

Güncelleştirilmiş Hello hizmet tanımı ve hizmet yapılandırma dosyalarını, dağıtımınızı tooAzure yükleme paketi. Kullanıyorsanız **cspack**, kullanmayan **/generateConfigurationFile** , eklediğiniz sertifika bilgilerini üzerine yazar olarak bayrak.

## <a name="step-3-upload-a-certificate"></a>3. adım: bir sertifikayı karşıya yüklemek
Dağıtım paketi güncelleştirilmiş toouse hello sertifika bırakıldı ve bir HTTPS uç nokta eklenir. Şimdi hello paketini ve sertifika tooAzure hello Klasik Azure portalı ile karşıya yükleyebilirsiniz.

1. İçinde toohello oturum [Klasik Azure portalı][Azure classic portal]. 
2. Tıklatın **bulut Hizmetleri** hello sol taraftaki gezinti bölmesi.
3. İstenen hello bulut hizmeti'ı tıklatın.
4. Merhaba tıklatın **sertifikaları** sekmesi.
   
    ![Merhaba sertifikalar sekmesini tıklatın](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. Merhaba tıklatın **karşıya** düğmesi.
   
    ![Karşıya Yükle](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. Merhaba sağlamak **dosya**, **parola**, ardından **tam** (onay işareti hello).

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>4. adım: toohello rol HTTPS kullanarak bağlanın
Dağıtımınızı Azure'da da çalışır durumda, HTTPS kullanarak tooit bağlanabilir.

1. Buna Klasik Azure portalı Merhaba, dağıtımınızı seçin, ardından altında hello bağlantısına tıklayın **Site URL'si**.
   
   ![Site URL'si belirleme][2]
2. Web tarayıcınızda hello bağlantı toouse değiştirme **https** yerine **http**ve başlangıç sayfasını ziyaret edin.
   
   > [!NOTE]
   > Merhaba otomatik olarak imzalanan sertifika ile ilişkili tooan HTTPS uç noktası göz attığınızda kendinden imzalı bir sertifika kullanıyorsanız, bir sertifika hatası hello tarayıcıda görebilirsiniz. Bir güvenilen sertifika yetkilisi tarafından imzalanmış bir sertifika kullanarak bu sorunları ortadan kaldırılır; Hello bu arada, hello hatayı yoksayabilirsiniz. (Başka bir seçenek tooadd hello otomatik olarak imzalanan sertifika toohello kullanıcının güvenilen sertifika yetkilisi sertifika deposunda olur.)
   > 
   > 
   
   ![SSL örnek web sitesi][3]

Hazırlama dağıtımı yerine Üretim dağıtımı için toouse SSL istiyorsanız, ilk dağıtım hazırlama hello için kullanılan toodetermine hello URL gerekir. Bulut hizmeti toohello hazırlama ortamınızı bir sertifika veya sertifika bilgileri dahil etmeden dağıtın. Uygulama dağıtıldıktan sonra hello Klasik Azure Portalı'nın listelendiğini hello GUID tabanlı URL belirleyebilirsiniz **Site URL'si** alan. Merhaba ortak adı (CN) eşit toohello GUID tabanlı URL ile bir sertifika oluşturun (örneğin, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**). Bulut hizmeti kullanım hello Azure Klasik portalı tooadd hello sertifika tooyour hazırlanır. Ardından, CSDEF ve CSCFG hello sertifika bilgileri tooyour dosyaları ekleyin, uygulamanızın yeniden paketleyin ve aşamalı dağıtım toouse hello yeni paketinizi güncelleştirin.

## <a name="next-steps"></a>Sonraki adımlar
* [Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure.md).
* Nasıl çok öğrenin[bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy.md).
* Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name.md).
* [Bulut hizmetinizi yönetme](cloud-services-how-to-manage.md).

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
