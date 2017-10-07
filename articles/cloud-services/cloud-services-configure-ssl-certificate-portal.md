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
# <a name="configuring-ssl-for-an-application-in-azure"></a>Azure'da bir uygulama için SSL yapılandırma
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-configure-ssl-certificate-portal.md)
> * [Klasik Azure Portalı](cloud-services-configure-ssl-certificate.md)
>

Güvenli Yuva Katmanı (SSL) şifreleme yöntemidir hello gönderilen veri korumanın en yaygın olarak kullanılan hello Internet. Bu ortak görev ele alınmaktadır nasıl toospecify web rolü nasıl tooupload bir SSL sertifikası ve toosecure uygulamanız için bir HTTPS uç nokta.

> [!NOTE]
> Bu görevde Hello yordamlar tooAzure bulut Hizmetleri uygulanır; Uygulama hizmetleri için bkz: [bu](../app-service-web/web-sites-configure-ssl-certificate.md).
>

Bu görev, bir üretim dağıtımı kullanır. Hazırlama dağıtımı hakkında bilgi hello bu konunun sonunda sağlanır.

Okuma [bu](cloud-services-how-to-create-deploy-portal.md) henüz bir bulut hizmeti oluşturmadıysanız, ilk.

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

<a name="modify"> </a>

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

3. Hizmet tanımı dosyasında eklemek bir **bağlama** öğesi hello içinde **siteleri** bölümü. Bu öğe bir HTTPS bağlama toomap uç nokta tooyour site ekler:

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

   Tüm hello gerekli değişiklikleri toohello hizmet tanımı dosyası tamamlandı; Ancak, yine de tooadd hello sertifika bilgilerini hello hizmet yapılandırma dosyası gerekir.
4. Hizmet yapılandırma dosyanızdaki (CSCFG) ServiceConfiguration.Cloud.cscfg, ekleme bir **sertifikaları** , sertifikanızın değerle. Merhaba aşağıdaki kod örneği ayrıntılarını hello sunan **sertifikaları** hello parmak izi değeri dışında bölümü.

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

(Bu örnekte **sha1** hello parmak izi algoritması için. Merhaba sertifikanızın parmak izi algoritması için uygun değeri belirtin.)

Güncelleştirilmiş Hello hizmet tanımı ve hizmet yapılandırma dosyalarını, dağıtımınızı tooAzure yükleme paketi. Kullanıyorsanız **cspack**, kullanmayan **/generateConfigurationFile** yeni eklediğiniz sertifika bilgilerini üzerine yazar olarak bayrak.

## <a name="step-3-upload-a-certificate"></a>3. adım: bir sertifikayı karşıya yüklemek
Toohello Azure portalına bağlanmak ve...

1. Merhaba, **tüm kaynakları** hello portalı bölümünde, bulut hizmeti seçin.

    ![Bulut hizmetinizi yayımlayın](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. Tıklatın **Sertifikalar**.

    ![Merhaba sertifikaları simgesine tıklayın](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. Tıklatın **karşıya** hello sertifikaları alanının hello üstünde.

    ![Merhaba karşıya yükleme menü öğesini tıklatın](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. Hello sağlamak **dosya**, **parola**, ardından **karşıya** hello altındaki hello veri giriş alanı.

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>4. adım: toohello rol HTTPS kullanarak bağlanın
Dağıtımınızı Azure'da da çalışır durumda, HTTPS kullanarak tooit bağlanabilir.

1. Merhaba tıklatın **Site URL'si** tooopen hello web tarayıcısı ayarlama.

   ![Merhaba Site URL'Sİ'ı tıklatın](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. Web tarayıcınızda hello bağlantı toouse değiştirme **https** yerine **http**ve başlangıç sayfasını ziyaret edin.

   > [!NOTE]
   > Merhaba otomatik olarak imzalanan sertifika ile ilişkili tooan HTTPS uç noktası göz attığınızda kendinden imzalı bir sertifika kullanıyorsanız, bir sertifika hatası hello tarayıcıda görebilirsiniz. Bir güvenilen sertifika yetkilisi tarafından imzalanmış bir sertifika kullanarak bu sorunları ortadan kaldırılır; Hello bu arada, hello hatayı yoksayabilirsiniz. (Başka bir seçenek tooadd hello otomatik olarak imzalanan sertifika toohello kullanıcının güvenilen sertifika yetkilisi sertifika deposunda olur.)
   >
   >

   ![Site Önizleme](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > Hazırlama dağıtımı yerine Üretim dağıtımı için toouse SSL istiyorsanız, önce dağıtım hazırlama hello için kullanılan toodetermine hello URL gerekir. Bulut hizmetinizi dağıtıldıktan sonra ortam hazırlama hello URL toohello hello tarafından belirlenir **dağıtım kimliği** bu biçiminde GUID:`https://deployment-id.cloudapp.net/`  
   >
   > Merhaba ortak adı (CN) eşit toohello GUID tabanlı URL ile bir sertifika oluşturun (örneğin, **328187776e774ceda8fc57609d404462.cloudapp.net**). Bulut hizmeti kullanım hello portal tooadd hello sertifika tooyour hazırlanır. Ardından, CSDEF ve CSCFG hello sertifika bilgileri tooyour dosyaları ekleyin, uygulamanızın yeniden paketleyin ve aşamalı dağıtım toouse hello yeni paketinizi güncelleştirin.
   >

## <a name="next-steps"></a>Sonraki adımlar
* [Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure-portal.md).
* Nasıl çok öğrenin[bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy-portal.md).
* Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name-portal.md).
* [Bulut hizmetinizi yönetme](cloud-services-how-to-manage-portal.md).
