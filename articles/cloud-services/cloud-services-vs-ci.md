---
title: "Bulut için aaaContinuous teslim hizmetleri Visual Studio Online ile | Microsoft Docs"
description: "Bilgi nasıl tooset Azure için sürekli teslimini bulut uygulamaları depolama anahtar toohello hizmet yapılandırma dosyalarını tanılama kaydetmeden"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a>Securely bulut Hizmetleri tanılama depolama anahtarı Kaydet ve Visual Studio Online kullanarak kurulum sürekli tümleştirme ve dağıtım tooAzure
 Ortak bir yöntem tooopen kaynak projeleri günümüzde olur. Güvenlik açıklarını Ortak kaynak denetimlerinden sızmasını gizli kullanıma sunulan gibi uygulama parolaları yapılandırma dosyaları kaydetme artık güvenli uygulamadır. Paylaşılan kaynaklar hello bulut ortamında yapı sunucuları olabileceği gerçeğidir ya da düz metin sürekli tümleştirme ardışık düzen dosyasında güvenli olmadığından gizli depolama. Bu makalede nasıl Visual Studio ve Visual Studio Online azaltır hello güvenlik sorunlarının geliştirme ve sürekli tümleştirme işlemi sırasında açıklanmaktadır.

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a>Proje yapılandırma dosyasında tanılama depolama anahtarını gizli kaldırın
Bulut Hizmetleri tanılama uzantısını Tanılama sonuçları kaydetmek için Azure depolama alanı gerektirir. Önceden hello depolama bağlantı dizesi hello bulut Hizmetleri Yapılandırma (.cscfg) dosyalarında belirtilir ve toosource denetimine iade edilemedi. Merhaba son Azure SDK sürümündeki kısmi bir bağlantı dizesi bir belirteç tarafından değiştirilen hello anahtarla hello davranışı tooonly deposu değiştirildi. Aşağıdaki adımları hello hello yeni bulut Hizmetleri Araçları nasıl çalıştığını açıklar:

### <a name="1-open-hello-role-designer"></a>1. Merhaba rol Tasarımcısı'nı açın
* Çift tıklatın veya bir bulut Hizmetleri rolü tooopen rol designer'ı sağ tıklatın

![Rolü Aç Tasarımcısı][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a>2. Tanılama bölümü altında yeni bir onay kutusu "çıkartmayın depolama anahtarı projeden gizli" eklenir
* Merhaba yerel depolama öykünücüsü kullanıyorsanız, UseDevelopmentStorage olan hello yerel bağlantı dizesi için gizli hiçbir toomanage olduğundan bu onay kutusunu devre dışı = true.

![Yerel depolama öykünücüsü bağlantı dizesi gizli değil][1]

* Yeni bir proje oluşturuyorsanız, varsayılan olarak bu onay kutusu işaretli değildir. Bu, seçili hello depolama bağlantı dizesi bir belirteç ile değiştirilen hello depolama anahtar bölüm sonuçlanır. Merhaba hello belirteç değerini hello geçerli kullanıcının AppData gezici klasörü altında örneğin bulunacaktır: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService

> Bu hello user\AppData klasör erişim kontrol kullanıcı oturum açma tarafından ve güvenli bir yerde toostore geliştirme gizli olarak kabul edilir unutmayın.
> 
> 

![Depolama anahtarı kullanıcı profili klasörü altında kaydedilir][2]

### <a name="3-select-a-diagnostics-storage-account"></a>3. Bir tanılama depolama hesabı seçin
* "..." Merhaba tıklayarak başlatılan hello iletişim kutusundan bir depolama hesabı seçin tıklayın. Oluşturulan hello depolama bağlantı dizesi nasıl hello depolama hesabı anahtarı sahip olmaz dikkat edin.
* Örneğin: DefaultEndpointsProtocol = https; AccountName = contosostorage; AccountKey = $(*clouddiagstrg.key*)

### <a name="4----debugging-hello-project"></a>4.    Merhaba projeyi hata ayıklama
* Visual Studio'da hata ayıklamayı F5 toostart. Her şeyi hello aynı çalışmalıdır eskisi yolu.
  ![Yerel olarak hata ayıklama başlatılamıyor][3]

### <a name="5-publish-project-from-visual-studio"></a>5. Visual Studio'da projeyi yayımlama
* Başlatma hello yayımlama iletişim kutusu ve oturum açma yönergeleri toopublish hello applicaion tooAzure ile devam edin.

### <a name="6-additional-information"></a>6. Ek bilgiler
> Not: hello Ayarları panelini hello rol Tasarımcısı'nda şu an için olduğu gibi kalır. Tanılama için toouse hello gizli yönetimi özelliği istiyorsanız toohello yapılandırmaları sekmesine gidin.
> 
> 

![Ayarları Ekle][4]

> Not: etkinleştirilirse, hello Application Insights anahtar düz metin olarak depolanır. hiçbir hassas verilerin güvenliğinin bozulması riskini risk altında olacak hello anahtar yalnızca karşıya yükleme içeriği için kullanılır.
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a>Derleme ve bir bulut Hizmetleri'ni Visual Studio online görev şablonları kullanarak projeyi yayımlama
* Aşağıdaki adımları hello gösterilmektedir toosetup bulut Hizmetleri için sürekli tümleştirme nasıl proje Visual Studio online görevler kullanma:
  ### <a name="1----obtain-a-vso-account"></a>1.    VSO hesabı elde etme
* [Visual Studio Online hesabı oluşturma] [ Create Visual Studio Online account] zaten yoksa,
* [Takım projesi oluşturma] [ Create team project] Visual Studio online hesabınızda

### <a name="2----setup-source-control-in-visual-studio"></a>2.    Visual Studio'da kurulum kaynak denetimi
* Tooa takım projesine bağlanma

![Tooteam projesine bağlanın][5]

![Takım projesi tooconnect seçin][6]

* Proje toosource denetim ekleme

![Proje toosource denetim ekleme][7]

![Harita proje tooa kaynak denetimi klasörü][8]

* Takım Gezgini'nden projenizdeki denetleyin

![Proje toosource denetiminde denetleyin][9]

### <a name="3----configure-build-process"></a>3.    Derleme işlemi yapılandırma
* Tooyour takım projesine göz atın ve yeni bir derleme işlem şablonları Ekle

![Yeni bir derleme ekleyin][10]

* Select derleme görevi

![Yapı görev ekleme][11]

![Visual Studio derleme görevi şablonu seçin][12]

* Yapı görev girişi düzenleyin. Lütfen tooyour göre parametreleri hello yapı özelleştirme

![Derleme görevi yapılandırın][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* Yapı değişkenleri yapılandırın

![Yapı değişkenleri yapılandırın][14]

* Bir görev tooupload derleme bırakma ekleme

![Seçin derleme bırakma görevi yayımlama][15]

![Yapılandırma derleme bırakma görevi yayımlama][16]

* Merhaba yapı çalıştırın

![Yeni yapıyı sıraya al][17]

![Yapı özetini görüntüle][18]

* Merhaba yapı başarılı ise sonucu benzer toobelow görürsünüz

![Sonuç derleme][19]

### <a name="4----configure-release-process"></a>4.    Yayın işlem yapılandırma
* Yeni bir sürüm oluşturma

![Yeni sürüm oluşturma][20]

* Hello Azure Cloud Services Dağıtımı görev seçin

![Azure Cloud Services Dağıtımı görev seçin][21]

* Merhaba depolama hesabı anahtarı toosource denetiminde denetlenmedi olarak toospecify hello gizli anahtarı tanılama uzantıları ayarlamak için ihtiyacımız var. Merhaba genişletin **yeni hizmet oluşturmak için Gelişmiş Seçenekleri** bölümünde ve hello Düzenle **tanılama depolama hesabı anahtarlarını** parametresi giriş. Anahtar değer çifti hello biçiminde birden fazla satır, bu girdi alır **[RoleName]:$(StorageAccountKey)**

> Not: Merhaba bulut Hizmetleri uygulaması burada yayımlayacak olarak aynı abonelik altında depolama hesabıdır, tanılama Merhaba, hello dağıtım görev girişinde tooenter hello anahtar gerekmez; Merhaba dağıtım aboneliğinizden program aracılığıyla hello depolama bilgi edinir
> 
> 

![Bulut Hizmetleri dağıtım görev yapılandırın][22]

* Kullanım gizli depolama anahtarları değişkenleri toosave oluşturun. bir değişken gizli olarak tıklatın hello kilit simgesini hello hello sağ tarafındaki toomask değişkenleri giriş

![Gizli derleme değişkenleri depolama anahtarları Kaydet][23]

* Sürüm oluşturma ve proje tooAzure dağıtma

![Yeni sürüm oluşturma][24]

## <a name="next-steps"></a>Sonraki adımlar
Azure bulut Hizmetleri için tanılama uzantıları ayarlama hakkında daha fazla toolearn lütfen bkz. [PowerShell kullanarak Azure Cloud Services tanılamayı etkinleştirme][Enable diagnostics in Azure Cloud Services using PowerShell]

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
