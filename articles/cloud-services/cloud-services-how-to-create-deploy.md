---
title: "aaaHow toocreate ve bir bulut hizmeti dağıtma | Microsoft Docs"
description: "Bilgi nasıl toocreate ve Azure'da hello hızlı oluşturma yöntemini kullanarak bir bulut hizmeti dağıtın."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 09f889f81ccee6e8a7657116183aa4100410214c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Nasıl tooCreate ve bir bulut hizmeti dağıtma
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-create-deploy-portal.md)
> * [Klasik Azure Portalı](cloud-services-how-to-create-deploy.md)
> 
> 

Merhaba Klasik Azure portalı toocreate sizin için iki yöntem sağlar ve bir bulut hizmetinin dağıtılacağı: **hızlı Oluştur** ve **özel Oluştur**.

Bu konuda nasıl toouse hızlı oluşturma yöntemini toocreate yeni bir bulut hizmeti hello ve ardından açıklanmaktadır **karşıya** tooupload ve Azure bulut hizmet paketinde dağıtma. Bu yöntemi kullandığınızda, hello Klasik Azure portalı gittiğiniz gibi tüm gereksinimleri tamamlamak için kullanılabilir uygun bağlantılar sağlar. Bulut hizmet oluşturduğunuzda hazır toodeploy değilseniz, hem hello yapabilirsiniz kullanarak aynı zaman **özel Oluştur**.

> [!NOTE]
> Bulut hizmeti Visual Studio Team Services (VSTS) gelen toopublish planlıyorsanız, kullanın **hızlı Oluştur**ve ardından VSTS yayımlama ayarlama **Hızlı Başlangıç** veya hello Pano.
> 
> 

## <a name="concepts"></a>Kavramlar
Üç bileşenler bir uygulama olarak bir bulut hizmeti Azure'da sipariş toodeploy gereklidir:

* **Hizmet tanımı**  
  Merhaba bulut Hizmet tanım dosyası (.csdef) rollerini hello sayısı dahil olmak üzere hello hizmet modeli tanımlar.
* **Hizmet yapılandırması**  
  Merhaba bulut hizmet yapılandırma dosyasının (.cscfg) hello bulut hizmeti ve bireysel rolleri rol örnekleri hello sayısı dahil olmak üzere, yapılandırma ayarlarını sağlar.
* **Hizmet paketi**  
  Merhaba hizmet paketi (.cspkg) hello uygulama kodu ve yapılandırmaları ve hello hizmet tanımı dosyası içerir.

Bunlar hakkında daha fazla bilgi edinmek ve nasıl toocreate bir paket [burada](cloud-services-model-and-package.md).

## <a name="prepare-your-app"></a>Uygulamanızı hazırlama
Bir bulut hizmeti dağıtmadan önce uygulama kodunuz ve bir bulut hizmet yapılandırma dosyasının (.cscfg) hello bulut hizmet paketi (.cspkg) oluşturmanız gerekir. Hello Azure SDK'sı, bu gerekli dağıtım dosyaları hazırlamak için araçlar sağlar. Merhaba SDK hello yükleyebilirsiniz [Azure indirmeleri](https://azure.microsoft.com/downloads/) sayfa olan uygulama kodunuz toodevelop tercih hello dilde.

Bir hizmet paketi vermeden önce üç bulut hizmeti özellikleri özel yapılandırmalar gerektirir:

* Veri şifreleme için Güvenli Yuva Katmanı (SSL) kullanan bir bulut hizmeti toodeploy istiyorsanız [uygulamanızı yapılandırma](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) SSL için.
* Tooconfigure Uzak Masaüstü bağlantıları toorole örnekleri, isterseniz [hello rollerini yapılandırma](cloud-services-role-enable-remote-desktop.md) Uzak Masaüstü için.
* Tooconfigure ayrıntılı bulut hizmetiniz için izleme istiyorsanız Azure tanılama hello bulut hizmeti için etkinleştirin. *Minimum izleme* (Merhaba varsayılan düzeyi izleme) hello ana bilgisayar işletim sistemlerinden rol örnekleri (sanal makineler) için toplanan performans sayaçlarını kullanır. "Ayrıntılı izleme * hello rol örnekleri tooenable yakın analizini uygulama işlemi sırasında oluşabilecek sorunları içinde performans verilerine göre ek ölçümleri toplar. toofind nasıl tooenable Azure tanılama Bkz [Azure etkinleştirme tanılamada](cloud-services-dotnet-diagnostics.md).

toocreate web rolleri veya çalışan rolleri dağıtımlarına sahip bulut hizmeti, şunları yapmalısınız [hello hizmet paketi oluşturma](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Başlamadan önce
* Hello Azure SDK'sı yüklemediyseniz tıklatın **Azure SDK Yükle** tooopen hello [Azure indirmeler sayfası](https://azure.microsoft.com/downloads/)ve hello SDK, tercih ettiğiniz toodevelop kodunuzu hello dil için karşıdan yükleyin. (Bu bir fırsat toodo sahip olacaksınız daha sonra.)
* Tüm rol örneklerinin bir sertifika gerektiriyorsa, hello sertifikaları oluşturur. Bulut Hizmetleri bir .pfx dosyası özel bir anahtarla gerektirir. Yapabilecekleriniz [hello sertifikaları tooAzure karşıya](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) hello bulut hizmeti oluşturup gibi.
* Toodeploy hello bulut hizmeti tooan benzeşim grubu planlıyorsanız hello benzeşim grubu oluşturun. Bulut hizmetiniz ve diğer Azure Hizmetleri toohello bir benzeşim grubu toodeploy kullanabileceğiniz bir bölgede aynı konumu. Hello hello benzeşim grubu oluşturabilirsiniz **ağlar** hello hello üzerinde Klasik Azure portalı alanı **benzeşim grupları** sayfası.

## <a name="how-to-create-a-cloud-service-using-quick-create"></a>Nasıl yapılır: Hızlı oluşturma yöntemini kullanarak bir bulut hizmeti oluştur
1. Merhaba, [Klasik Azure portalı](http://manage.windowsazure.com/), tıklatın **yeni**>**işlem**>**bulut hizmeti** > **Hızlı Oluştur**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. İçinde **URL**, üretim dağıtımlarında bulut hizmetinize erişmek için bir alt etki alanı adı toouse hello ortak URL girin. Üretim dağıtımları için Hello URL biçimi: http://*myURL*. cloudapp.net.
3. İçinde **bölge veya benzeşim grubunda**, hello coğrafi bölge veya benzeşim grubunda toodeploy hello bulut hizmetine seçin. Bulut hizmeti toohello toodeploy istiyorsanız bir benzeşim grubu seçin bir bölgedeki diğer Azure hizmetleriyle aynı konumda.
4. **Bulut Hizmeti Oluştur**’a tıklayın.
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    Merhaba ileti alanı hello pencerenin hello altındaki hello işleminde hello durumunu izleyebilirsiniz.
   
    Merhaba **bulut Hizmetleri** alanı açılır ve görüntülenen hello yeni bulut hizmeti ile. Merhaba durumu tooCreated değiştiğinde, bulut hizmeti oluşturma başarıyla tamamlandı.
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a>Nasıl yapılır: bir bulut hizmeti için bir sertifika karşıya yükle
1. Merhaba, [Klasik Azure portalı](http://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**hello bulut hizmeti hello adına tıklayın ve ardından **Sertifikalar**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. Ya da tıklatın **bir sertifika karşıya** veya **karşıya**.
3. İçinde **dosya**, kullanın **Gözat** tooselect hello sertifika (.pfx dosyası).
4. İçinde **parola**, hello hello sertifikanın özel anahtarı girin.
5. Tıklatın **Tamam** (onay işareti).
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    Aşağıda gösterilen hello karşıya yükleme hello ileti alanında hello ilerlemesini izleyebilirsiniz. Merhaba karşıya yükleme tamamlandığında, hello sertifika toohello tablo eklenir. Merhaba ileti alanına Tamam tooclose selamlama iletisine tıklayın.
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a>Nasıl yapılır: bir bulut hizmeti dağıtma
1. Merhaba, [Klasik Azure portalı](http://manage.windowsazure.com/), tıklatın **bulut Hizmetleri**hello bulut hizmeti hello adına tıklayın ve ardından **Pano**.
2. Ya da tıklatın **yeni bir üretim dağıtımı karşıya** veya **karşıya**.
3. İçinde **dağıtım etiketi**, hello yeni dağıtım - Örneğin, MyCloudServicev4 için bir ad girin.
4. İçinde **paket**, kullanın **Gözat** tooselect hello hizmet paketi dosyasının (.cspkg) toouse.
5. İçinde **yapılandırma**, kullanın **Gözat** tooselect hello hizmet yapılandırma dosyasının (.cscfg) toouse.
6. Merhaba bulut hizmeti herhangi bir rol ile yalnızca bir örnek içeriyorsa, hello seçin **bir veya daha fazla rol tek bir örnek içeriyorsa bile Dağıt** onay kutusunu tooenable hello dağıtım tooproceed.
   
    Her role en az iki örnek varsa azure yalnızca 99,95 yüzde erişim toohello bulut hizmeti Bakım ve hizmet güncelleştirmeleri sırasında garanti edebilir. Gerekirse, ek rol örnekleri üzerinde hello ekleyebilirsiniz **ölçek** hello bulut hizmeti dağıttıktan sonra sayfa. Daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).
7. Tıklatın **Tamam** (onay işareti) toobegin hello bulut hizmeti dağıtımı.
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    Merhaba hello ileti alanında hello dağıtım durumunu izleyebilirsiniz. Tamam toohide selamlama iletisine tıklayın.
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a>Başarıyla tamamlandı, dağıtımı doğrulama
1. Tıklatın **Pano**.
   
    Merhaba durum hello hizmet olduğunu göstermelidir **çalıştıran**.
2. Altında **Hızlı Bakış**, bulut hizmetiniz bir web tarayıcısında hello site URL'si tooopen'ı tıklatın.
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a>Sonraki adımlar
* [Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure.md).
* Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name.md).
* [Bulut hizmetinizi yönetme](cloud-services-how-to-manage.md).
* Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate.md).

