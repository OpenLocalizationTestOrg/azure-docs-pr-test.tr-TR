---
title: "aaaCreate Hello World için bir bulut hizmeti Eclipse ile Azure"
description: "Nasıl basit bir Hello World uygulaması kullanarak toocreate hello Eclipse için Azure Araç Seti öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 7262e705-59d6-43ce-b888-29a21c8e0cb7
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: dfb81374aaf78e933c0bf83a1dbd98023801491a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a>Eclipse'te Azure için bir Hello World bulut hizmeti oluştur
Merhaba aşağıdaki adımlarda size yol gösterecektir toocreate ve hello Azure araç setini Eclipse için kullanarak temel bir JSP uygulaması tooAzure dağıtın. Kolaylık olması için bir JSP örneği gösterilir, ancak Azure dağıtım ilgili olduğu kadar yüksek oranda benzer adımlar bir Java servlet için uygun olacaktır.

Merhaba uygulaması benzer toohello aşağıdaki görünür:

![][ic600360]

## <a name="prerequisites"></a>Ön koşullar
* Bir Java Geliştirme Seti (JDK), v 1,7 veya üzeri.
* Java EE geliştiricileri için Eclipse IDE Indigo olarak biliniyordu veya üzeri. Bu adresten yüklenebilir <http://www.eclipse.org/downloads/>.
* Java tabanlı web sunucusu ya da Apache Tomcat, GlassFish, JBoss uygulama sunucusu, Jetty veya IBM® WebSphere® uygulama sunucusu özgürlük çekirdek gibi uygulama sunucusu dağıtımı.
* Öğesinden alınan bir Azure aboneliği <http://azure.microsoft.com/pricing/purchase-options/>.
* Eclipse için Azure Araç Seti Hello. Daha fazla bilgi için bkz: [yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse].

## <a name="toocreate-a-hello-world-application"></a>toocreate Merhaba Dünya uygulaması
İlk olarak, bir Java projesi oluşturma ile başlayacağız devre dışı.

1. Eclipse başlatın ve başlangıç menüsünde tıklatın **dosya**, tıklatın **yeni**ve ardından **dinamik Web projesi**. (Görmüyorsanız **dinamik Web projesi** tıkladıktan sonra kullanılabilir bir proje listelenen **dosya**, **yeni**, ardından aşağıdaki hello: tıklatın **dosya**, tıklatın **yeni**, tıklatın **proje...** , genişletin **Web**, tıklatın **dinamik Web projesi**, tıklatıp **sonraki**.)

1. Bu öğreticinin amaçları doğrultusunda hello proje adı **MyHelloWorld**. (Emin bu adı kullanın, bu öğreticide sonraki adımlarda beklediğiniz MyHelloWorld adlı, WAR dosyasını toobe). Ekranınızın benzer toohello aşağıdaki görünür:

   ![][ic589576]

1. **Son**'a tıklayın.

1. Eclipse'nın Proje Gezgini görünümü içinde genişletmek **MyHelloWorld**. **WebContent**'e sağ tıklayın, **Yeni**'ye tıklayın ve ardından **JSP Dosyası**'na tıklayın.

1. Merhaba, **yeni JSP dosyası** iletişim, adı hello dosyası **index.jsp**. Merhaba üst klasörünü olarak **MyHelloWorld/WebContent**hello aşağıda gösterildiği gibi:

   ![][ic659262]

1. Merhaba, **JSP şablon seç** iletişim kutusunda, Bu öğretici seçin amacıyla **yeni JSP dosyası (html)** tıklatıp **son**.

1. Merhaba index.jsp dosyası Eclipse'te açıldığında, metin toodynamically görünümünde eklemek **Merhaba Dünya!** Merhaba varolan içinde `<body>` öğesi. Güncelleştirilmiş `<body>` içerik hello aşağıdaki gibi görünmelidir:
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. İndex.jsp kaydedin.

## <a name="toodeploy-your-application-tooazure-hello-quick-and-simple-way"></a>toodeploy uygulama tooAzure, hello hızlı ve basit bir yol
Bir Java web uygulaması hazır tootest alır almaz, out doğrudan Azure hello üzerinde bulut kısayol tootry aşağıdaki hello kullanabilirsiniz.

1. Eclipse'nın Proje Gezgini'nde tıklatın **MyHelloWorld**.

2. Merhaba Hello Eclipse araç çubuğunda tıklatın **Yayımla** aşağı açılan düğme ve ardından **Azure bulut hizmeti olarak Yayımla**

   ![][publishDropdownButton]

3. Bu uygulama tooAzure hello için ilk kez yayımlama ve önce bu uygulama için bir Azure dağıtım projesi oluşturmadıysanız, bir Azure dağıtım projesi sizin için otomatik olarak oluşturulması. Merhaba komut isteminde, aynı zamanda otomatik olarak olacak hello JDK paket ve uygulama sunucusu listeleyen aşağıdaki toorun uygulamanızı dağıttınız görmeniz gerekir.

   ![][ic789598]
   
   Bu kısayol yaklaşım, belirli sunucu veya hello varsayılan adlardan farklı JDK tooconfigure gerek kalmadan, Azure uygulamanızda hızlı ve kolay bir şekilde tootest sağlar. Merhaba öndeğerlerini memnun kaldığınızda, tıklayabilirsiniz **Tamam** toocontinue aşağıdaki adımları hello ile.
   Ancak, toochange istiyorsanız hello JDK veya uygulama sunucusu toouse uygulamanız için yapabilirsiniz, daha sonra sizin için otomatik olarak oluşturulan hello Azure dağıtım projesi düzenleyerek veya tıklatabilirsiniz **iptal** şimdi ve okuma Merhaba **hakkında Azure dağıtım projeleri bölüm** Bu öğreticinin.

4. Merhaba, **tooAzure yayımlama** iletişim:

   1. Hello abonelikleri tooselect varsa **abonelik** liste henüz abonelik bilgilerinizi bu adımları tooimport izleyin:
      1. Tıklatın **yayımlama ayarları dosyasını içeri aktar**.
      2. Merhaba, **alma abonelik bilgilerini** iletişim kutusunda, tıklatın **yayımlama ayarları dosyası karşıdan**. Azure hesabınızda henüz tutulmaz içinde istendiğinde toolog olacaktır. Size sorulacaktır sonra toosave Azure yayımlama ayarları dosyası. Tooyour yerel makine kaydedin.
      3. Merhaba yine de **alma abonelik bilgilerini** iletişim kutusunda, hello tıklatın **Gözat** düğmesi, select hello yayımlama hello önceki adımda yerel olarak kaydedilmiş ayarları dosyası ve ardından  **Açık**. Ekranınızın benzer toohello aşağıdaki gibi görünmelidir:![][ic644267]
      4. **Tamam** düğmesine tıklayın.
   2. İçin **abonelik**, dağıtımınız için kullanmak istediğiniz hello abonelik seçin.
   3. İçin **depolama hesabı**, toouse istediğiniz veya tıklatın hello depolama hesabını seçin **yeni** toocreate yeni bir depolama hesabı.
   4. İçin **hizmet adı**, toouse istediğiniz veya tıklatın hello bulut hizmeti seçin **yeni** toocreate yeni bir bulut hizmeti.
   5. İçin **hedef işletim sistemi**seçin toouse dağıtımınız için istediğiniz hello hello işletim sistemi sürümü.
   6. İçin **hedef ortam**, bu öğreticinin amaçları seçmek için **hazırlama**. (Hazır toodeploy tooyour üretim sitesini olduğunuzda, bu çok değiştireceğiz**üretim**.)
   7. İsteğe bağlı: emin **önceki dağıtım üzerine** üzerine yaz'ı, yeni dağıtım tooautomatically istiyorsanız, önceki dağıtım hello denetlenir. Bu seçeneği etkinleştirdiğinizde, değil deneyimi "409 çakışma" sorunları toohello yayımlarken olur aynı konumu.
      Bu hello Not **tooAzure yayımlama** iletişim için bir bölüm içeren **uzaktan erişim**. Varsayılan olarak, uzaktan erişim etkin değildir ve biz, bu örnek için izin vermez. tooenable uzaktan erişim, uzaktan oturum açarken kullanıcı adı ve parola toouse girmeniz gerekir. Uzaktan erişim hakkında daha fazla bilgi için bkz: [eclipse'te Azure dağıtımları için uzaktan erişim etkinleştirme][Enabling Remote Access for Azure Deployments in Eclipse].
      **TooAzure yayımlama** iletişim benzer toohello aşağıdaki görünecektir:![][ic719488]

5. Tıklatın **Yayımla** toopublish toohello hazırlama ortamı.

   İstendiğinde tooperform tam bir yapı tıklattığınızda **Evet**. Bu hello ilk yapı için birkaç dakika sürebilir.
   Bir **Azure etkinlik günlüğü** sekmeli Eclipse Görünümler bölümünde görüntülenir.
   ![][ic719489]Bu günlüğü kullanmak yanı sıra hello **konsol** toosee hello ilerlemeyi dağıtımınızın görüntüleme. Toohello toolog alternatiftir [Azure Yönetim Portalı][Azure Management Portal]ve hello **bulut Hizmetleri** bölümünde toomonitor hello durumu.

6. Dağıtımınız başarılı bir şekilde dağıtıldığında, hello **Azure etkinlik günlüğü** durumunu gösterecektir **yayımlanan**. Tıklatın **yayımlanan**görüntü ve tarayıcınız dağıtımınızı örneği açılır hello aşağıdaki gösterildiği gibi.

   ![][ic719490]

Bu ortam hazırlama dağıtım tooa olduğundan hello DNS adı hello form http:// olacaktır&lt;*GUID*&gt;. cloudapp.net ve hello URL hello DNS adı ve uygulamanız için bir son eke içerecek. Örneğin, http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld. (Merhaba **MyHelloWorld** bölümü duyarlıdır.) Merhaba DNS de görebilirsiniz hello dağıtım adı hello Azure platformu Yönetim Portalı (içinde hello bulut Hizmetleri bölümü hello Yönetim Portalı'nın) tıklatırsanız adı.

Ortamı hazırlama dağıtım toohello için bu gözden geçirme olmasına rağmen bir dağıtım tooproduction izleyen hello aynı adımları dışında hello içinde **tooAzure yayımlama** iletişim kutusunda **üretim** yerine **hazırlama** hello için **hedef ortam**. Hazırlama için kullanılan bir GUID yerine tercih ettiğiniz hello DNS adına göre bir URL dağıtım tooproduction sonuçlanır.

> [!WARNING]
> Bu noktada, Azure uygulamanızı toohello bulut dağıtmış. Ancak, devam etmeden önce çalışmadığı olsa bile, dağıtılan bir uygulama tooaccrue Faturalanabilir zaman aboneliğinize ilişkin devam edecek farkında olun. Bu nedenle, Azure aboneliğinizden istenmeyen dağıtımları silin son derece önemlidir.
> 
> 

## <a name="about-azure-deployment-projects"></a>Azure dağıtım projeleri hakkında
İçinde bir veya daha fazla Java uygulamaları tooAzure toodeploy sipariş, bir Azure dağıtım projesi gereklidir. Merhaba, uygulamalarınızın Azure üzerinde yayımlanan sipariş toobe içine sarmalanmış toobe gerekir "paketi" Merhaba rolü oynar.

Merhaba yanı sıra hakkında bilgi uygulamalarınızı, bir Azure dağıtım projesi ayrıca diğer anahtar bileşenler hakkında bilgi, dağıtımınızın en önemlisi içerir: uygulama sunucusu kapsayıcı toorun web uygulamanızda hello ve Java Çalışma zamanı toorun Merhaba, . Azure Java Çalışma zamanları ve Java uygulama sunucuları aralarından seçim yapabileceğiniz büyük seçimi destekler.

Burada kullanılan Merhaba örneği eğitim amaçlı olarak büyük ölçüde basitleştirilmiş karşın, bir Azure dağıtım projesi toocreate neredeyse rasgele karmaşık, ölçeklenebilir, yüksek oranda kullanılabilir etkinleştirir diğer önemli yapılandırma bilgilerini de içerebilir, uygulamalarınızı çok katmanlı bulut hizmetleriyle. Etkinleştirebilirsiniz **oturum benzeşimi ("Yapışkan oturumları")**, **hızlı önbelleğe alma**, **SSL boşaltma**, **güvenlik duvarı/bağlantı noktası yönlendirme**, **uzaktan erişim**ve diğer güçlü özellikleri sayısı.

Bu öğreticinin önceki bölümde hello tamamladığınıza varsa ("toodeploy uygulama tooAzure, hello hızlı ve basit bir yol"), bir yeni proje Gezgini sizin için otomatik olarak oluşturulur ve adlı hello Azure dağıtım projesine şimdi göreceksiniz " **MyHelloWorld_onAzure**".

Ayrıca bu öğreticinin ilk boş Azure dağıtım projesi kendiniz oluşturma ve uygulamaları tooit ekleyerek başlattığınız. Bir uzun olduğundan işlem ancak hello başlangıç yapılandırmasını hello başından üzerinde daha fazla denetim sağlar.

toocreate, sıfırdan yeni bir Azure dağıtım projesi tıklatın hello **yeni Azure dağıtım projesi** düğmesini ![][ic710876].

Olup, zaten varolan bir Azure dağıtım projesi ile çalışma veya bir sıfırdan oluşturma, bağımsız olarak mümkün toochange yapılandırma ayarlarını ve hello JDK gibi bileşenleri olan veya uygulama sunucusu, aynı kolaylıkla hello dilediğiniz zaman.

toochange hello JDK, veya hello uygulama sunucusu ya da var olan bir Azure dağıtım projesi hello uygulama listesinde:

1. Başlangıç projesi düğümünü genişletin (örneğin **MyHelloWorld_onAzure**) hello Proje Gezgini içinde

2. Sağ **WorkerRole1**

3. Merhaba genişletin **Azure** hello bağlam menüsünde alt

4. Tıklatın **sunucu yapılandırması**

Bağımsız olarak, yukarıda gösterildiği gibi mevcut bir Azure dağıtım projesi düzenleyerek bu sunucu yapılandırma adımları başlattığınız ya da sıfırdan yeni bir tane oluşturmak, hello görürsünüz aynı iletişimleri tooconfigure izin vererek, JDK sunucusu ve uygulama yazın bileşenleri. daha nasıl toochange hello ayarları bu iletişim kutuları, örneğin toochange hello JDK, hello uygulama sunucusu ve eklemek veya bir dağıtımda, uygulamaları kaldırmak toolearn bkz hello [sunucu yapılandırma özellikleri] [ Server configuration properties] makalesi.

## <a name="windows-only-toodeploy-your-application-toohello-compute-emulator"></a>Yalnızca Windows: toodeploy uygulama toohello işlem öykünücüsü

> [!NOTE]
> Hello Azure öykünücüsü, yalnızca Windows üzerinde kullanılabilir. Windows dışındaki bir işletim sistemi kullanıyorsanız, bu bölümü atlayabilirsiniz.
> 
> 

Daha önce yani örtük olarak, uygulama tooAzure yayımlayarak açıklanan başlangıç adımları izleyerek yeni bir Azure dağıtım projesi oluşturduysanız JDK hello ve uygulama sunucuları hello bulut için ancak yerel öykünmesi için yapılandırılır. tooprepare projenizi hello yerel öykünücüde test etmek için aşağıdaki adımları izleyin:

1. Eclipse'nın Proje Gezgini'nde tıklatın **MyHelloWorld_onAzure**.

2. Sağ **WorkerRole1**.

3. Merhaba genişletin **Azure** hello bağlam menüsünde alt.

4. Tıklatın **sunucu yapılandırması**.

5. Merhaba üzerinde **JDK** sekmesinde, hello Araç Seti varsayılan önceden yapılandırılmış olmadığını denetleyin, yerel JDK. Değilse veya Varsayılanları kabul toochange hello istiyorsanız, o hello olun **yerel olarak test etmek için bu dosya yolundan kullanım hello JDK** onay kutusu işaretli ve hello toouse istediğiniz JDK yükleme konumu belirtildi. Toochange istiyorsanız, hello tıklatın **Gözat** düğmesini tıklatın ve hello Gözat Denetimi'ni kullanarak hello JDK toouse hello dizin konumu seçin.

6. Merhaba tıklatın **Server** sekmesi.

7. Merhaba, **yerel sunucu yolu** hello iletişim kutusunun hello alttaki metin kutusu hello türü ve hello hello iletişim kutusunun üstündeki altında seçili hello sunucusu ana sürüm numarası eşleşen yerel olarak yüklenmiş bir sunucu hello yolunu girin Merhaba **bu tür bir sunucu dağıtımı** onay kutusu. Farklı tür veya hello uygulama sunucusu ana sürümüne toouse istiyorsanız, o onay kutusunu altında hello seçimi ilk değiştirin.

8. **Tamam** düğmesine tıklayın.

9. Merhaba Hello Eclipse araç çubuğunda tıklatın **Azure öykünücüsünde çalıştırın** düğmesini ![][ic710879]. Merhaba, **Azure öykünücüsünde çalıştırın** düğmesi etkin değil, emin **MyHelloWorld_onAzure** Eclipse'nın Proje Gezgini'nde seçilir ve Eclipse'nın Proje Gezgini odak hello olarak sahip olduğundan emin olun Geçerli penceresini açın. Bu ilk tam bir yapı projenizin başlatın ve Java web uygulamanızı hello işlem öykünücüsü başlatın. (Bilgisayarınızın performans özellikleri, bağlı olarak hello ilk yapı birkaç saniye tooa arasında birkaç dakika sürebilir, ancak sonraki oluşturur, Not daha hızlı alırsınız.) Merhaba ilk derleme adımı tamamlandıktan sonra ister Windows kullanıcı hesabı denetimi (UAC) tooallow tarafından bu komut toomake tooyour bilgisayar değiştirir. **Evet**'e tıklayın.

> [!IMPORTANT]
> Merhaba UAC simgesi için Windows görev çubuğunda hello ve ilk tıklatın hello UAC komut istemi, onay görmüyorsanız. Bazen hello UAC istemi en üstteki bir pencere olarak görünmez, ancak yalnızca bir görev çubuğunda simge olarak görünür.
> 
> 

1. Projenizi herhangi bir sorun varsa hello işlem öykünücüsü UI toodetermine hello çıktısını inceleyin. Dağıtımınızın Merhaba içeriğine bağlı olarak, tam olarak hello işlem öykünücüsü içinde başlatılan, uygulama toobe için birkaç dakika sürebilir.

2. Tarayıcınızı başlatın ve hello URL kullanmak `http://localhost:8080/MyHelloWorld` hello adresi olarak (Merhaba `MyHelloWorld` hello URL'sinin büyük küçük harfe duyarlı). MyHelloWorld uygulama (index.jsp çıkışını hello), görüntü aşağıdaki benzer toohello görmelisiniz:

   ![][ic589579]

Merhaba Eclipse araç çubuğunda, hello işlem öykünücüsü çalışmasını uygulamanız hazır toostop olduğunuzda hello'ı tıklatın **Azure öykünücüsünü sıfırlayın** düğmesini ![][ic710880].

## <a name="toodelete-your-deployment"></a>toodelete dağıtımınızı
toodelete dağıtımınızı hello Azure araç setini Eclipse için içinde emin **MyHelloWorld_onAzure** olan Eclipse'nın Proje Gezgini'nde seçili, hello Eclipse Proje Gezgini odaklanmanıza ve ardından geçerli pencereyi hello olduğundan emin olun Merhaba **yayımdan** düğmesini ![][ic710883], hello Eclipse araç. (Yapabilirsiniz, hello aynı işlem sağ tıklayarak **MyHelloWorld_onAzure** tıklatarak Eclipse'nın Proje Gezgini'nde **Azure** ve ardından **Azure bulutaUndeploy**.) Bu hello görüntüler **yayımdan Azure projesi** iletişim.

![][ic719491]

Dağıtım, toodelete istediğiniz ve ardından select hello dağıtım içerir hello abonelik ve bulut hizmeti seçin **yayımdan**.

(Bir alternatif toousing hello Araç Seti toodelete hello toouse hello dağıtımıdır **bulut Hizmetleri** hello Azure Yönetim Portalı bölümünde: tooyour dağıtım gidin, onu seçin ve hello ardından **Sil** düğmesi. Bu durdurmak ve ardından silin, hello dağıtım. Yalnızca toostop hello dağıtım istiyorsanız ve onu silmemeniz hello tıklatın **durdurmak** hello yerine düğmesini **silmek** hello dağıtım, Faturalanabilir ücretleri silmezseniz, yukarıda açıklanan ancak düğmesi, Dağıtımınız için tooaccrue devam) bile durdurulursa kullanılır.

## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse] 

[Yeni hello Eclipse için Azure Araç Seti nedir][What's New in hello Azure Toolkit for Eclipse]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic589576]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589576.png
[ic589579]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589579.png
[ic600360]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic600360.png
[ic644267]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic644267.png
[ic659262]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic659262.png
[ic710876]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710876.png
[ic710879]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710880.png
[ic710882]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710883.png
[ic719488]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719488.png
[ic719489]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719489.png
[ic719490]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719490.png
[ic719491]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719491.png
[ic789598]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic789598.png
[publishDropdownButton]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/publishDropdownButton.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690944.aspx -->
