---
title: "aaaCortana Intelligence AppSource yayımlama Kılavuzu | Microsoft Docs"
description: "Microsoft Partner toofollow toopublish Cortana Intelligence çözüm tooAppSource gerek duyduğunuz tüm hello adımlar şunlardır."
services: machine-learning
documentationcenter: 
author: AnupamMicrosoft
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: anupams;v-bruham;garye
ms.openlocfilehash: 66f26016b5eb709c567e9829aa787ca926e13d9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-appsource-publishing-guide"></a>Cortana Intelligence AppSource yayımlama Kılavuzu

## <a name="overview"></a>Genel Bakış
AppSource iş karar alıcılar (BDMs) toodiscover tek hedefi hello ve sorunsuz bir şekilde işletme çözümleri/iş ortakları tarafından oluşturulmuş ve Microsoft tarafından değerlendirilen uygulamalar deneyin. Gözcü [bu videoyu](https://youtu.be/hpq_Y9LuIB8) toolearn AppSource nasıl çalışır. 

Microsoft Partner varsa üzerinde AppSource yayımlama gerçekten yararlı olabilir:
- Bir akıllı çözüm/uygulama kullanılarak oluşturulan [Cortana Intelligence Suite](https://azure.microsoft.com/en-us/suites/cortana-intelligence-suite/?cdn=disable).
- Çözüm ya da uygulama belirli iş sorunu giderir.
- Modülleri veya müşterilerinize oldukça hızlı bir şekilde tahmin edilebilir bir şekilde yeniden kullanabilirsiniz fikri mülkiyet yerleşiktir.

Bir göz atalım [Cortana Intelligence çözümleri](https://appsource.microsoft.com/en-us/marketplace/apps?product=cortana-intelligence&page=1) , zaten yayımlanır AppSource üzerinde. 

Bu makalede hello adımları tooget bir iş ortağı yol Cortana Intelligence çözüm tooAppSource öğesinin yayımlanan

## <a name="getting-started"></a>Başlarken
1. Merhaba, [Partner topluluğunun avantajları Kılavuzu](https://www.microsoftpartnerserverandcloud.com/_layouts/download.aspx?SourceUrl=Hosted%20Documents/Partner%20Community%20Benefits%20Guide%20-%20Cloud%20and%20Enterprise.pdf) (PDF), sayfa 9 tooget Advanced Analytics iş ortağı olarak listelenen bakın.
1. Tam hello [uygulamanızı gönderme](https://appsource.microsoft.com/en-us/partners/list-an-app) formu.

    Merhaba soru için *"uygulamanız için yerleşik Seç hello ürünleri*", hello denetleyin **diğer** onay ve hello "Cortana Intelligence" listesinde düzenleme denetimi.
1. Cortana Intelligence uygulama edildi tooAppSource sağlayabilmek için önce Cortana Intelligence'nın iş ortağı çözümü teknolojisi ekibi tarafından sertifikalı gerekir. işlemi başlatıldı tooget, anket doldurarak uygulamanızı Lütfen paylaşım ayrıntılarını forma [Cortana Intelligence çözüm değerlendirme AppSource yayımlama](https://aka.ms/cisappsrceval). Bu site parola korumalı olup hello site nasıl tooget hello parola hakkında yönergeler içerir.

## <a name="solution-evaluation-criteria"></a>Çözüm değerlendirme ölçütleri
Ölçüt hello uygulama gereksinimlerini toomeet hello listesi aşağıdadır
1. Uygulamanın tooaddress belirli iş kullanım örneği sorun belirli bir işlev alanda önceden tanımlanmış değer önermeleri için en düşük yapılandırmaları ile tekrarlanabilir bir şekilde implementable kısa bir süre içinde gerekir.
1. Çözüm bileşenlerini aşağıdaki hello en az birini kullanmanız gerekir:

    - HDInsight
    - Machine Learning
    - Data Lake Analytics
    - Akış Analizi
    - Bilişsel hizmetler
    - Robot Altyapısı
    - Analysis Services
    - Microsoft R Server tek başına bekleme
    - R hizmetlerinde SQL 2016 ya da Hdınsight Premium
1. En az $1000 DPOR/CSP kullanarak müşteri ayda bir çözüm oluşturmak.
1. Çözüm (AAD Federasyon SSO) hello Azure Active Directory Federasyon tek oturum açma kullanıcı kimlik doğrulaması ve kaynak erişim denetimleri için etkin onay kullanmalısınız. Uygulamanızı edildi tooAppSource çalıştırılmadan önce etkin SSO çözümünüzün AAD olduğunu takım Federasyon tooshow toohello değerlendirme gerekir.

     toosee toobe AAD ne anlama geldiğini Federasyon SSO etkin, tooposition 02:35 arama [AppSource deneme sürümü deneyimi için size yol](https://aka.ms/trialexperienceforwebapps) video. Uygulamanız ile etkin değilse SSO AAD Federasyon henüz, ilgili bazı belgelerde İşte
   1. [Tek tıklamayla oturum açma](https://identity.microsoft.com/Landing?ru=https://identity.microsoft.com/).
   1. [Uygulamaları Azure Active Directory ile tümleştirme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application).
     
1. Power BI çözümünüzde kullanın: isteğe bağlıdır, ancak müşteri adayları daha yüksek sayıda toogenerate kanıtlanmış önemle önerilir.

## <a name="devcenter-account-setup"></a>DevCenter hesabı kurulumu
Bu, şirket toobecome bir yayımcı Microsoft'a kaydolma hello işlemidir. Kayıtlı bir yayımcı ile DevCenter hesabınız zaten varsa, DevCenter hesabınızla ilişkili hello e-posta kimliği paylaşır. Uygulamanızı yayımlama için onaylandıktan sonra erişim toofull belgelerine karşılaşırsınız [yayımcı profil bulut Portal yönetme](https://cloudpartner.azure.com/#documentation/manage-publisher-profile)

Yoksa, hello anahtar adımları toosetup DevCenter hesabı altındadır.
1. Bir Microsoft hesabı oluşturmak [burada](https://signup.live.com/signup.aspx).
1. Toohello Microsoft DevCenter Git [kayıt sayfası](http://go.microsoft.com/fwlink/?LinkId=615100) "kaydolun"'a tıklayın.
1. Ödeme için istendiğinde, biz tooyou sağlanan hello kodunu kullanın. Bir kod yoksa, kişi [ appsourcecissupport@microsoft.com ](mailto:appsourcecissupport@microsoft.com?subject=Request%20for%20promotion-code%20for%20DevCenter%20account%20setup).
1. Select hello [ülke/bölge](https://docs.microsoft.com/windows/uwp/publish/account-types-locations-and-fees) yaşadığınız veya işletmenizin bulunduğu. **Mümkün toochange olmayacaktır bu daha sonra.**
1. Seçin, [Geliştirici hesap türü](https://docs.microsoft.com/windows/uwp/publish/account-types-locations-and-fees) için AppSource, select **şirket**. Bir şirket hesabı için emin tooreview bunlar olması [yönergeleri](https://docs.microsoft.com/windows/uwp/publish/opening-a-developer-account).
1. Geliştirici hesabınız için toouse istediğiniz hello kişi bilgilerini girin.
Ayrıntılı adım adım yönergeleri nasıl toosetup DevCenter hesabı bkz hello yönergeleri [burada](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-accounts-creation-registration).

## <a name="provide-info-for-microsoft-sellers"></a>Microsoft satıcıları için bilgilerini belirtin
İş ortakları için AppSource, hello anahtar değer önermeleri toobe mümkün toocollaborate Microsoft Sellers ile iş ortağı uygulamalarını potansiyel müşterilerle önünde konumlandırma biridir.

Doldurup [Microsoft Sellers için iş ortağı çözümü bilgisi](https://aka.ms/aapartnerappinfo) ve çok gönderme[appsourcecissupport@microsoft.com](mailto:appsourcecissupport@microsoft.com?subject=Request%20publisher%20account%20creation%20for%20%3cPartner%20Name%3e%20and%20whitelist%20owner/contributer%20AAD/MSA%20email%20IDs). Bu yayımlama için onaylanan Cortana Intelligence uygulama tooget için gerekli adımdır.

## <a name="build-a-compelling-customer-walkthrough-on-appsource"></a>İlgi çekici bir müşteri kılavuz üzerinde AppSource derleme
İlk olarak, bir göz atalım [Neal Analytics stok iyileştirme](https://appsource.microsoft.com/en-us/product/web-apps/neal_analytics.8066ad01-1e61-40cd-bd33-9b86c65fa73a?tab=Overview&tag=CISHome) AppSource üzerinde. AppSource her uygulama giriş için bir deneme sürümü deneyimi pdf belgelerini girişi dışında'nın üzerine başlık, özeti (en fazla 100 karakter), açıklama (max 1300 karakter), görüntüler, videoları (isteğe bağlı) sahiptir. İş ortakları, tüm bu toobuild ilgi çekici bir müşteri deneyimi faydalanın.

İş ortakları, bir son tooend satış orchestration olarak AppSource üzerinde koyarlar hello içeriğinin düşünmelisiniz. Müşteriler hello başlığı ve açıklamayı toounderstand hello değer teklifinde okuyun ve hangi hello çözüm hakkındadır görüntüleri & videolar toounderstand aracılığıyla gidin. Örnek olay incelemeleri müşterilerinizin nasıl Mevcut müşterileri görmek olası değer alınıyor. 

Tüm bu hello müşteri olmalısınız ilgilenen ve isteyen tooknow daha fazla eşitleyerek. Bu aralık tabanlı deste sunu iyi teknik satış temsilcisi hello yeni müşteriler size yol olarak düşünün. Merhaba önerilen biçimidir açıklaması toobreak değer önermeleri bağlı alt bölümlerine hello metni, her biri vurgulanmış olan bir alt başlık. 

Ziyaretçilerin genellikle hangi hello uygulama adresleri, hello "Özet sunan" alanı ve alt başlıklar tooget gist genel bakış ve neden bunlar düşünmelisiniz hello uygulamada yalnızca hızlı bir bakış. Bu nedenle, tooget hello kullanıcının dikkat edin bunları neden tooread tooget hello özellikleri üzerinde önemlidir.

Bu iş ortaklarının yapmış olmanız bakın.
- [Neal Analytics stok en iyi duruma getirme](https://appsource.microsoft.com/en-us/product/web-apps/neal_analytics.8066ad01-1e61-40cd-bd33-9b86c65fa73a?tab=Overview)
- [Plexure perakende kişiselleştirme](https://appsource.microsoft.com/en-us/product/web-apps/plexure.c82dc2fc-817b-487e-ae83-1658c1bc8ff2?tab=Overview)
- [AvePoint Citizen Hizmetleri](https://appsource.microsoft.com/en-us/product/web-apps/avepoint.7738ac97-fd40-4ed3-aaab-327c3e0fe0b3?tab=Overview)

Merhaba son satış tooshow hello uygulama/çözümünün nasıl hello değer teklifinde teslim gösteren bir tanıtım işlemidir. Tam olarak bir müşteri deneme sürümü deneyimi AppSource üzerinde için tasarlanmıştır olmasıdır. İyi bir tanıtım ne yapacağını hello aşağıdaki:
- Merhaba değer teklifinde hello uygulamanın kısa yeniden özetlemek ve hello kişiler hello çözümü ile etkileşime hello müşteri kesin içinde kullanıma listesi
- Öykü ve kümelerini hello bağlam belirli sorunlarla ilgilenen bir örnek müşteri hakkında bilgi verin
- Nasıl hello durum genellikle devolve ve hello çözüm kullanımda olduğunda ne olacağını hello müşteri (önce) VS etkisi açıklanmaktadır. Bu Power BI panoları vb. kullanarak gösterilebilir.
- Nasıl hello çözüm herhangi belirli Machine Learning algoritmaları vb. kullanarak durum kolaylaştırır özetler.

içinde AppSource eklenen hello içerik kaliteli olmalıdır ve yeterli tooenable hello aşağıdaki yukarı Dikiş:
- Bir iş ortağının teknik satış insanların kendi satış düzenlemesi kullanıyor olması gerekir. Satış ekipleriniz kullanmadan da mümkün toodo olan MS satış terimleri aynı hello bekleyebilirsiniz iyi bir oturum olur. Bu iletişim müşteri noktası etkinleştirecek toobe mümkün tooconsistently geçiş hello aynı Öykü tootheir takım mates ve daha yüksek ups tooget bütçe ve onaylar önce bir satın alma işlem yapılabilir.
- Hello site organik bir şekilde ziyaret müşteri hello tüm başlarına içerik gidin ve Çoğalması toorespond geri toopartner iletişimi toomove sonraki adımlara devam eşitleyerek.

İş ortakları düşünmek neden, içerik AppSource bir bitiş tooend satış orchestration olarak üzerinde koyarlar hello olduğu. Merhaba Öykü satır ve deneme sürümü deneyimi gösterilen özellikleri toobe bağlı olarak, Teklif türü karar.

## <a name="publish-your-app-on-hello-publishing-portal"></a>Uygulamanızı yayımlama hello portalındaki yayımlayın
Biz, uygulamanız için yukarıdaki adımları hello hesaplanan sonra erişim toohello yayımlama portalında alırsınız ve görebilirsiniz [nasıl toopublish Cortana Intelligence teklif bulut iş ortağı portalı yoluyla](https://cloudpartner.azure.com/#documentation/cloud-partner-portal-publish-cortana-intelligence-app) sonraki adımlar hakkında ayrıntılı yönergeler için.

Merhaba alanlar hakkında bilgi gerekiyorsa, e-posta < appsourcecissupport@microsoft.com >.
## <a name="my-app-is-published-on-appsource---now-what"></a>Uygulamam AppSource üzerinde - yayımlanan şimdi ne?
İlk olarak, uygulamanızı alma Tebrikler yayımladı.
Merhaba hedef kitle nasıl etkileyeceğini uygulamanıza AppSource yoğun yayımlama alma döndürür Hello düzeyine bağlıdır. Bkz: [büyüme-korsan Cortana Intelligence uygulamanıza AppSource](http://aka.ms/aagrowthhackguide) nasıl, hello döndürür en üst düzeye hakkında daha fazla ayrıntı için.

Herhangi bir sorunuz varsa veya öneriler, lütfen ulaşmak adresindeki toous < appsourcecissupport@microsoft.com >.

