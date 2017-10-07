---
title: "aaaHow toocreate ve bir bulut hizmeti dağıtma | Microsoft Docs"
description: "Bilgi nasıl toocreate ve hello Azure portal kullanarak bir bulut hizmeti dağıtın."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Nasıl toocreate ve bir bulut hizmeti dağıtma
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-create-deploy-portal.md)
> * [Klasik Azure Portalı](cloud-services-how-to-create-deploy.md)
>
>

Hello Azure portal toocreate sizin için iki yöntem sağlar ve bir bulut hizmeti dağıtma: *hızlı Oluştur* ve *özel Oluştur*.

Bu makalede nasıl toouse hızlı oluşturma yöntemini toocreate yeni bir bulut hizmeti hello ve ardından açıklanmaktadır **karşıya** tooupload ve Azure bulut hizmet paketinde dağıtın. Bu yöntemi kullandığınızda, hello Azure portal, Git gibi tüm gereksinimleri tamamlamak için kullanılabilir uygun bağlantılar sağlar. Bulut hizmet oluşturduğunuzda hazır toodeploy değilseniz, hem hello yapabilirsiniz aynı anda özel Oluştur kullanma.

> [!NOTE]
> Bulut hizmeti Visual Studio Team Services (VSTS) gelen toopublish planlıyorsanız, hızlı Oluştur'u kullanın ve ardından VSTS yayımlama hello Azure hızlı başlangıç veya hello panosundan ayarlayın. Daha fazla bilgi için bkz: [kesintisiz teslim tooAzure kullanarak Visual Studio Team Services tarafından][TFSTutorialForCloudService], veya Merhaba yardımcı **Hızlı Başlangıç** sayfası.
>
>

## <a name="concepts"></a>Kavramlar
Gerekli toodeploy bir uygulamayı Azure bulut hizmeti olarak üç bileşeni vardır:

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

* Veri şifreleme için Güvenli Yuva Katmanı (SSL) kullanan bir bulut hizmeti toodeploy istiyorsanız [uygulamanızı yapılandırma](cloud-services-configure-ssl-certificate-portal.md#modify) SSL için.
* Tooconfigure Uzak Masaüstü bağlantıları toorole örnekleri, isterseniz [hello rollerini yapılandırma](cloud-services-role-enable-remote-desktop-new-portal.md) Uzak Masaüstü için.
* Tooconfigure ayrıntılı bulut hizmetiniz için izleme istiyorsanız Azure tanılama hello bulut hizmeti için etkinleştirin. *Minimum izleme* (Merhaba varsayılan düzeyi izleme) hello ana bilgisayar işletim sistemlerinden rol örnekleri (sanal makineler) için toplanan performans sayaçlarını kullanır. *Ayrıntılı izleme* hello rol örnekleri tooenable yakın analizini uygulama işlemi sırasında oluşabilecek sorunları içinde performans verilerine göre ek ölçümleri toplar. toofind nasıl tooenable Azure tanılama Bkz [Azure tanılama etkinleştirme](cloud-services-dotnet-diagnostics.md).

toocreate web rolleri veya çalışan rolleri dağıtımlarına sahip bulut hizmeti, şunları yapmalısınız [hello hizmet paketi oluşturma](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Başlamadan önce
* Hello Azure SDK'sı yüklemediyseniz tıklatın **Azure SDK Yükle** tooopen hello [Azure indirmeler sayfası](https://azure.microsoft.com/downloads/)ve hello SDK, tercih ettiğiniz toodevelop kodunuzu hello dil için karşıdan yükleyin. (Bu bir fırsat toodo sahip olacaksınız daha sonra.)
* Tüm rol örneklerinin bir sertifika gerektiriyorsa, hello sertifikaları oluşturur. Bulut Hizmetleri bir .pfx dosyası özel bir anahtarla gerektirir. Merhaba bulut hizmeti oluşturup gibi hello sertifikaları tooAzure karşıya yükleyebilirsiniz.

## <a name="create-and-deploy"></a>Oluşturma ve dağıtma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Tıklatın **yeni > işlem**, tooand tıklatın kaydırarak **bulut hizmeti**.

    ![Bulut hizmetinizi yayımlayın](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. Merhaba yeni içinde **bulut hizmeti** dikey penceresinde hello için bir değer girin **DNS adı**.
4. Yeni bir **kaynak grubu** veya varolan bir tanesini seçin.
5. Bir **Konum** seçin.
6. Tıklatın **paket**. Bu hello açar **bir paketi yükleme** dikey. Merhaba gerekli alanları doldurun. Rollerinizi hiçbirini tek bir örnek içeriyorsa, olun **bir veya daha fazla rol tek bir örnek içeriyorsa bile Dağıt** seçilir.
7. Olduğundan emin olun **Başlat dağıtım** seçilir.
8. Tıklatın **Tamam** hello kapatılacak **bir paketi yükleme** dikey.
9. Tüm sertifikaları tooadd yoksa tıklatın **oluşturma**.

    ![Bulut hizmetinizi yayımlayın](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a>Bir sertifikayı karşıya yüklemek
Dağıtım paketi varsa [toouse sertifikaları yapılandırılmış](cloud-services-configure-ssl-certificate-portal.md#modify), hello sertifika şimdi karşıya yükleyebilirsiniz.

1. Seçin **sertifikaları**ve hello **eklemek sertifikaları** dikey penceresinde hello SSL sertifika .pfx dosyasını seçin ve ardından hello sağlayın **parola** hello sertifika için
2. Tıklatın **Attach sertifika**ve ardından **Tamam** hello üzerinde **eklemek sertifikaları** dikey.
3. Tıklatın **oluşturma** hello üzerinde **bulut hizmeti** dikey. Merhaba dağıtım ulaşıldığında hello **hazır** durumu toohello sonraki adımlara geçebilirsiniz.

    ![Bulut hizmetinizi yayımlayın](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a>Başarıyla tamamlandı, dağıtımı doğrulama
1. Merhaba bulut hizmet örneği'ı tıklatın.

    Merhaba durum hello hizmet olduğunu göstermelidir **çalıştıran**.
2. Altında **Essentials**, hello tıklatın **Site URL'si** bulut hizmeti bir web tarayıcısında tooopen.

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a>Sonraki adımlar
* [Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure-portal.md).
* Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name-portal.md).
* [Bulut hizmetinizi yönetme](cloud-services-how-to-manage-portal.md).
* Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate-portal.md).
