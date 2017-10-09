---
title: "Öğretici: Hello Azure Portal ile DevOps | Microsoft Docs"
description: "Bilgi hello Azure Portal'ın çeşitli DevOps iş akışları hello."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a>Öğretici: Hello Azure Portal ile DevOps
Hello Azure platformu esnek DevOps iş akışları ile doludur. Bu öğreticide, nasıl tooleverage hello hello Azure Portal toodevelop özelliklerini sınamak, dağıtma, sorun giderme, izlemek ve çalışan uygulamaları yönetmek öğrenin. Bu öğretici hello aşağıdakilere odaklanır:

1. Bir web uygulaması oluşturma ve sürekli dağıtımı etkinleştirme
2. Uygulama geliştirme ve test etme
3. Bir uygulamayı izleme ve sorunlarını giderme
4. Genel uygulama yönetimi görevleri

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a>Bir web uygulaması oluşturma ve sürekli dağıtımı etkinleştirme
Bir Web uygulaması ile oluşturma [Azure App Service](https://azure.microsoft.com/services/app-service/), bu öğreticinin hello kalan kullanması. Başlangıçta kaynak kod deponuzdan çalışan Azure ortamımıza sürekli dağıtımı etkinleştirin.

1. Azure portalında oturum açın hello
2. Seçin **uygulama hizmetleri** &gt; **Ekle simgesi** ve bir ad girin, aboneliğinizi seçin ve yeni bir kaynak grubu tooserve hello hizmeti için hello kapsayıcı olarak oluşturun.
   
   Kaynak grupları toomanage izin hello çözüm faturalandırma, dağıtımlar ve aracılığıyla tek bir grup olarak tüm izleme gibi çeşitli yönlerini [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
   
   ![image1][image1]
3. Birkaç dakika sonra uygulama hizmetiniz oluşturulur. Birkaç dakika tooexplore hello hello hizmet çeşitli menü seçeneklerini hello Portalı'nda alın.
   
   ![image2][image2]    
4. Merhaba URL'yi tıklatın. Merhaba çeşitli havuzlar ve depolara mevcut seçeneklere dikkat edin. Merhaba dilleri ve çerçeveleri .NET, Java ve Ruby gibi seçtiğiniz de kullanabilirsiniz.
   
   ![image3][image3]    
5. Hello Azure portalı sürekli dağıtımı yalnızca birkaç basit adımdan oluşan kolay bir işlem yapar. Hello Azure portalı, yeni oluşturduğunuz hello uygulama hizmeti için hello simgesinden ayarlarını seçin.
   
   ![image4][image4]
   
   Merhaba sağ açar hello dikey penceresinden bölüm yayımlama toohello kaydırın.
   
   ![image5][image5]
6. Ardından, hello uygulaması için bazı ayarları tooenable sürekli dağıtım yapılandırın. Dağıtım Kaynağı’na ve ardından Kaynak Seç’e tıklayın. Merhaba çeşitli depo kaynakları için sahip olduğunuz seçeneklere dikkat edin.
   
   ![image6][image6]
7. Bu örnek için GitHub'ı seçin. İsteğe bağlı olarak, tercih ettiğiniz hello depoyu seçin ve hello yetkilendirme kimlik bilgilerini ayarlayın.
   
   ![image7][image7]
8. Yetkilendirme tooyour depo sonra bir proje ve toodeploy istediğiniz dalı seçebilirsiniz. Aşağıda birkaç hayali örnek listelenmiştir.
   
   ![image8][image8]
9. Projenizi ve dalınızı seçtikten sonra Tamam'a tıklayın. Bir dağıtımın bildirimlerini toosee başlamanız gerekir.
   
   ![image9][image9]
10. Toointegrate hello kaynak denetim deposunu Azure ile oluşturulan geri tooGitHub toosee hello Web kancası gidin. Hello Azure Portal yalnızca birkaç basit adımda GitHub ile tümleştirme sağlar.
    
    ![image10][image10]
11. toodemonstrate sürekli dağıtımı hızlıca bazı içerik toohello deposunu ekleyin. Basit bir örnek için bir örnek metin dosyası tooa GitHub deposuna ekleyin. Ücretsiz toouse .NET, Ruby, Python veya başka türden bir App Service uygulama var. Ücretsiz tooadd bir metin dosyası eşitleyerek tercih ettiğiniz ASP.NET MVC, Java ya da Ruby uygulaması toohello deposu.
    
    ![image11][image11]
12. Değişiklikleri tooyour depo uyguladıktan sonra yeni bir gördüğünüz dağıtım hello portal bildirimleri alanında başlatın. Hızlı bir şekilde değişiklikleri tooyour depo uyguladıktan sonra görmüyorsanız Eşitle'yi tıklatın.
    
    ![image12][image12]
13. Bu noktada, deneyin ve hello uygulama hizmeti hello sayfa yükleme, 403 hatası alabilirsiniz. Başlangıç sayfa dosyası index.htm veya default.html gibi için tipik varsayılan belge Kurulum olduğundan bu örnekte, bu değildir. Hızlı bir şekilde bu hello Azure Portal tooling hello ile çözebilirsiniz.  Ayarlar Hello Azure Portal'ı seçin &gt; uygulama ayarları.
    
     ![image13][image13]
14. Uygulama ayarları için bir dikey pencere açılır. Merhaba hello "SamplePage.html" sayfasının adını girin ve Kaydet'e tıklayın. Birkaç dakika tooexplore hello diğer ayarlar olur.
    
    ![image14][image14]
15. İsteğe bağlı olarak beklenen hello değişiklikleri görmek için tarayıcı URL tooensure yenileyin. Bu durumda, şimdi hello sayfayı dolduran bazı basit metinler yoktur. Her ek değişiklik toohello deposu içinde yeni bir otomatik dağıtım neden olur.
    
    ![image15][image15]
    
    Hello Azure Portal ile sürekli dağıtımın etkinleştirilmesi kolay bir deneyimdir. Ayrıca, daha karmaşık yayın işlem hatları oluşturabilir ve varolan kaynak denetimi ve otomatik derleme ve sürüm yönetimi sistemleri yararlanarak gibi sürekli tümleştirme sistemleri toodeploy tooAzure, diğer birçok tekniği kullanabilirsiniz.

## <a name="develop-and-test-an-app"></a>Uygulama geliştirme ve test etme
Ardından, bazı değişiklikler toohello kodu temel yapın ve bu değişiklikleri hızlıca dağıtın. Merhaba Web uygulaması için test bazı performans ayarlama Kurulum.

1. Hello Azure Portal hello Gezinti bölmesinden uygulama Hizmetleri'ni seçin ve App service'inizi bulun.
   
   ![image16][image16]
2. Araçlar'a tıklayın
   
   ![image17][image17]
3. Kategori Araçlar altındaki geliştirme hello dikkat edin. Bize hello Azure Portal ayrılmadan uygulamalarıyla toowork sağlayan birkaç faydalı araç burada vardır. Konsol'a tıklayın.
   
   ![image18][image18]
4. Merhaba konsol penceresinde uygulamanız için dinamik komutlar gönderebilirsiniz. Type hello dir komutunu ve isabet girin. Yükseltilmiş ayrıcalıklar gerektiren komutlar çalışmaz.
   
   ![image19][image19]
5. Toohello geliştirme kategorisine geri dönün ve Visual Studio Online'ı seçin. Note: Visual Studio Online artık Visual Studio Team Services olarak adlandırılmaktadır.
   
   ![image20][image20]
6. Merhaba tarayıcı içi düzenleme deneyimini uygulamanız için Değiştir'i tıklatın.
   
   ![image21][image21]
7. Uygulamanız için bir web uzantısı yüklenir. Uzantıları hızla ve kolayca Azure'da işlevselliği tooapps ekleyin. Merhaba bazıları kullanılabilir hello ekran görüntüsünde başka uzantı türleri dikkat edin.
   
   ![image22][image22]
8. Merhaba Visual Studio Online uzantısı yüklendikten sonra Git'e tıklayın.
   
   ![image23][image23]
9. Bir tarayıcı sekmesi geliştirme IDE'sini doğrudan hello tarayıcıda gördüğünüz açar. Aşağıdaki bildirim hello deneyim Chrome ' ' dir.
   
   ![image24][image24]
10. Dosya düzenleme gibi çeşitli etkinlikleri gerçekleştirmek, dosya ve klasör ekleyin ve hello Canlı siteden içerik indirme. Bir hızlı düzenleme toohello SamplePage.html dosya oluşturun.
    
    ![image25][image25]
11. Birkaç dakika sonra hello değişiklikler otomatik olarak kaydedilir. Geri toohello sayfa giderseniz, hello değişiklikleri görebilirsiniz. Bunlar gibi canlı düzenlemeler üretim ortamları için büyük olasılıkla uygun değildir. Ancak, hello Araçlar geliştirme için çok kolay toomake hızlı değişiklikler yapın ve sınama ortamlarında.
    
    ![image26][image26]
    
    ![image27][image27]
12. Toohello Araçlar dikey penceresine geri dönün ve hello geliştirme kategorisi altında performans Testi'ne tıklayın.
    
    ![image28][image28]
13. Tooset team services hesabı gerekir. Daha fazla ayrıntı için buraya bakın: [Team Services Hesabı Oluşturma](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
14. Yeni toocreate üzerinde bir performans testi'ı tıklatın.
    
    ![image29][image29]
    
    Yapılandırma çeşitli değerleri hello ve hello iletişim tooinitiate bir performans testi hello altındaki testi Çalıştır'ı tıklatın.
    
    ![image30][image30]
    
    ![image31][image31]
15. Merhaba test çalışmaya başladıktan sonra hello durumunu izleyebilirsiniz.
    
    ![image32][image32]
    
    Merhaba test tamamlandıktan sonra hello sonuca tıklandığında daha ayrıntılı bilgi gösterilir.
    
    ![image33][image33]
16. Bu örnekte, küçük bir test çalışması, sınırlı veri tooanalyze yoktur ancak sizin çeşitli ölçümleri görebilir yanı sıra testinizi bu görünümden yeniden oluşturuldu. Hello Azure Portal oluşturma, yürütme ve kolay bir işlem web performans testlerini çözümleme yapar. Merhaba ekran görüntüleri hello performans verilerini görüntüler.
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a>Bir uygulamayı izleme ve sorunlarını giderme
Azure, çalışan uygulamaları izleme ve sorunlarını gidermeye yönelik çok sayıda özellik sağlar.

1. Hello Azure Portal'da Web uygulamamız için Araçlar seçin.
   
   ![image37][image37]
2. Merhaba sorun giderme kategorisi altında çalışan bir uygulamayla araçları tootroubleshoot olası sorunları kullanma seçeneklerinin çeşitliliğine hello dikkat edin. Canlı HTTP trafiğini izleme, kendi kendini onarmayı etkinleştirme, günlükleri görüntüleme ve daha fazla işlemi yapabilirsiniz.
   
   ![image38][image38]
3. Site ölçümleri tooquickly get bazı HTTP kodlarına ilişkin bir görünüm seçin.
   
   ![image39][image39]
4. Hizmet Olarak Tanılama’yı seçin. Uygulamanızın türünü ve ardından Çalıştır'ı seçin.
   
   ![image40][image40]
   
   Bir koleksiyon başlar.
   
   ![image41][image41]
5. Merhaba uygun günlük toodiagnose olası sorunları seçebilirsiniz. HTTP günlükleri gibi tüm hello kullanılabilir veri seçeneklerini tooenable günlük toosee gerekir.
   
   ![image42][image42]
   
   Karşıdan yüklemek ve bir DebugDiag analiz hello bellek dökümü dosyasına tıklayarak analiz raporu toohelp olası sorunları bulma.
   
   ![image43][image43]
6. tooview daha fazla veri tooenable ek günlük gerekir. Hello Azure Portal, toohello Web uygulamasına gidin ve Ayarlar'ı seçin.
   
   ![image44][image44]
7. Toohello özellikler kategorisine kaydırın ve tanılama günlükleri'ni seçin.
   
      ![image45][image45]
8. Günlük için çeşitli seçenekler hello dikkat edin. Web sunucusu günlüğünü açın ve Kaydet'e tıklayın.
   
   ![image46][image46]
9. Hello uygulama toohello Araçlar alanına geri dönün ve hizmet olarak Tanılama'ı seçin ve Çalıştır toorerun hello veri toplama'ı tıklatın.
   
   ![image47][image47]
10. Merhaba HTTP günlüğü ayarı etkin HTTP günlükleri için toplanan verileri bakın.
    
    ![image48][image48]
11. Merhaba HTML dosya günlüğüne tıklayarak, daha fazla araştırma için zengin bir tarayıcı tabanlı rapor üretir.
    
    ![image49][image49]
12. Merhaba uygulaması için Azure Portal hello toohello Araçlar bölümüne geri dönün. Toohello Araçlar bölümüne kaydırın ve işlem Gezgini'ni seçin.
    
    ![image50][image50]
13. İşlem Gezgini'ni seçerek, çalışan işlemlere ilişkin ayrıntıları görüntüleyebilirsiniz. Aşağıda işlemlerin ayrıntılarına inebilir ve hatta tüm hello Azure Portal işlemlerini sonlandırın.
    
    ![image51][image51]
    
    ![image52][image52]
14. Merhaba soldaki toohello ayarları dikey geri dönün. Yeni destek isteği’ne tıklayın.
    
    ![image53][image53]
15. Merhaba sağ Hello dikey penceresinden, hello sorunlar hakkındaki ayrıntıları doldurun, kişi bilgilerini girin ve hatta tanılama verilerini karşıya yükleyebilirsiniz. Hello Azure Portal, Microsoft desteği ile sorunsuzca çalışmayı sağlar.
    
    ![image54][image54]
    
    ![image55][image55]
    
    Hello Azure Portal, güçlü ve bilindik deneyimleri toohelp İzleyici tooling sağlanmasına yardımcı olur ve çalışan uygulamalarımızı giderebilirsiniz. Siz de mümkün tootake eylem hızlı bir şekilde işlemleri geri dönüştürme, etkinleştirme ve çeşitli veri koleksiyonlarını devre dışı bırakma ve hatta Microsoft Profesyonel desteği ile tümleştirme gibi görevleri gerçekleştirerek olursunuz.

## <a name="general-application-management"></a>Genel Uygulama Yönetimi
Uygulamaları yönetirken çoğunlukla tooperform çok çeşitli yedekleme stratejilerini yapılandırma, uygulama ve kimlik sağlayıcılarını yönetme ve rol tabanlı erişim denetimini yapılandırma gibi etkinlikler gerekir. İle diğer DevOps deneyimlerinde hello gibi hello Azure platformu bu görevleri doğrudan hello portalda tümleştirir.

1. tutma tooensure hello Web uygulaması veri kaybına karşı güvenli, tooconfigure yedeklemeleri gerekir. Web uygulamanız için toohello ayarlar alanına gidin.
   
   ![image56][image56]
2. Merhaba sağ üzerinde Hello dikey penceresinde toohello özellikler kategorisine kaydırın.
   
    ![image57][image57]
3. Yedeklemeleri seçin; Merhaba doğru bir dikey pencere açılır.
   
   ![image58][image58]
4. Yapılandır'ı tıklatın, bir depolama hesabı hello sağ hello dikey penceresinde aşağıdakilerden birini seçin.
   
   ![image59][image59]
5. Şimdi oluşturun ve bir depolama kapsayıcısı toohold Yedeklemelerinizin seçin. Merhaba dikey penceresinde hello alt kısmındaki Oluştur'u tıklatın. Ardından hello kapsayıcısı seçin.
   
   ![image60][image60]
6. Merhaba kapsayıcıyı seçtikten sonra zamanlamaları gibi yedeklerini veritabanınız için yapılandırabilirsiniz. Bu senaryo için hello Kaydet simgesine tıklayın.
   
    ![image61][image61]
7. Kaydettikten sonra yedeklemeler için hello sol geri toohello dikey penceresini kaydırarak. Şimdi Yedekle tooback hello uygulama'yı tıklatın.
   
    ![image62][image62]
8. Birkaç dakika içinde bir yedeğin oluşturulduğunu görürsünüz. Bildirim hello hello aşağıdaki ekran görüntüsünde şimdi geri yükle seçeneğini.
   
    ![image63][image63]
9. Şimdi Geri Yükle'yi tıklatın ve hello seçenekleri toohello dikey penceresinde hello sağ inceleyin. Bir uygun yedekleme ve kolayca geri yükleme tooan önceki gerektiğinde durum seçebilirsiniz. Hello Azure portal bize kolayca hello uygulama için bir basit olağanüstü durum kurtarma stratejisi etkinleştirmek Yardım.
   
    ![image64][image64]
10. Merhaba soldaki ve Özellikler altında toohello ayarları dikey geri dönün ve kimlik doğrulama/Yetkilendirme'yi seçin.
    
     ![image65][image65]
11. Merhaba dikey penceresinde hello sağ App Service kimlik doğrulaması seçin. Merhaba çeşitli popüler sağlayıcılar ile yapılandırabileceğiniz seçeneklere dikkat edin.
    
     ![image66][image66]
12. Tercih ettiğiniz Hello sağlayıcıyı seçin ve hello kapsam hello seçeneklerini dikkat edin. Bir uygulama kimliği ve uygulama gizli anahtarı sağlayın ve hızlı bir şekilde hello uygulama için Facebook kimlik doğrulamasını etkinleştirin. Hello Azure Portal uygulamaları için hazır bir çözüm olarak kimlik doğrulamasını etkinleştirir.
    
     ![image67][image67]
13. Toohello ayarları dikey geri dönün ve hello kaynak yönetimi kategorisi altında kullanıcılar'ı seçin.
    
     ![image68][image68]
14. Merhaba dikey penceresinde hello sağ içinde inceleyin rol ve kullanıcı eklemek için çeşitli seçenekler hello. Hello Azure Portal hello uygulama için RBAC (rol tabanlı erişim denetimi) kolayca denetlemenize olanak tanır.
    
     ![image69][image69]

## <a name="summary"></a>Özet
Hızlı bir şekilde bir web uygulaması için sürekli dağıtımı etkinleştirme, çeşitli geliştirme gerçekleştirme ve etkinlikleri test, izleme ve canlı uygulama sorunlarını giderme ve son olarak anahtarını yönetme tarafından bu öğreticinin hello Azure platformu ile Merhaba güç bazıları gösterilmektedir Olağanüstü durum kurtarma, kimlik ve rol tabanlı erişim denetimi gibi stratejiler. Hello Azure platformu bu DevOps iş akışları için tümleşik bir deneyim sağlar ve elinizdeki hello görev bağlamının kalarak verimli bir şekilde çalışabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* Azure Resource Manager DevOps hello Azure platformu üzerinde etkinleştirilmesi için önemlidir.  toolearn daha ziyaret [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).
* Azure uygulama hizmeti dağıtımı hakkında daha fazla ziyaret toolearn [, uygulama tooAzure uygulama hizmeti dağıtma](../app-service-web/web-sites-deploy.md)

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
