---
title: "Eclipse'te Azure için bir Hello World bulut hizmeti oluştur"
description: "Eclipse için Azure Araç Seti kullanarak basit bir Hello World uygulamasının nasıl oluşturulacağını öğrenin."
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
ms.openlocfilehash: 9b31f0faeb6ee7b5e7b8fe3a1f2827133d6188e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a>Eclipse'te Azure için bir Hello World bulut hizmeti oluştur
Aşağıdaki adımlar Eclipse için Azure Araç Seti kullanarak oluşturmak ve temel bir JSP uygulaması azure'a dağıtma gösterir. Kolaylık olması için bir JSP örneği gösterilir, ancak Azure dağıtım ilgili olduğu kadar yüksek oranda benzer adımlar bir Java servlet için uygun olacaktır.

Uygulama şuna benzer görünür:

![][ic600360]

## <a name="prerequisites"></a>Ön koşullar
* Bir Java Geliştirme Seti (JDK), v 1,7 veya üzeri.
* Java EE geliştiricileri için Eclipse IDE Indigo olarak biliniyordu veya üzeri. Bu adresten yüklenebilir <http://www.eclipse.org/downloads/>.
* Java tabanlı web sunucusu ya da Apache Tomcat, GlassFish, JBoss uygulama sunucusu, Jetty veya IBM® WebSphere® uygulama sunucusu özgürlük çekirdek gibi uygulama sunucusu dağıtımı.
* Öğesinden alınan bir Azure aboneliği <http://azure.microsoft.com/pricing/purchase-options/>.
* Eclipse için Azure Araç Seti. Daha fazla bilgi için bkz: [Azure araç setini Eclipse için yükleme][Installing the Azure Toolkit for Eclipse].

## <a name="to-create-a-hello-world-application"></a>Merhaba Dünya uygulaması oluşturmak için
İlk olarak, bir Java projesi oluşturma ile başlayacağız devre dışı.

1. Eclipse başlatın ve menüsünde tıklatın **dosya**, tıklatın **yeni**ve ardından **dinamik Web projesi**. (Görmüyorsanız **dinamik Web projesi** tıkladıktan sonra kullanılabilir bir proje listelenen **dosya**, **yeni**, aşağıdakileri yapın: tıklatın **dosya**, tıklatın **yeni**, tıklatın **proje...** , genişletin **Web**, tıklatın **dinamik Web projesi**, tıklatıp **sonraki**.)

1. Bu öğreticinin amaçları doğrultusunda, proje adı **MyHelloWorld**. (Emin bu adı kullanın, bu öğreticide sonraki adımlarda beklediğiniz MyHelloWorld adlandırılması, WAR dosyası). Ekranınızın aşağıdakine benzer görünür:

   ![][ic589576]

1. **Son**'a tıklayın.

1. Eclipse'nın Proje Gezgini görünümü içinde genişletmek **MyHelloWorld**. **WebContent**'e sağ tıklayın, **Yeni**'ye tıklayın ve ardından **JSP Dosyası**'na tıklayın.

1. İçinde **yeni JSP dosyası** iletişim kutusunda, dosya adı **index.jsp**. Üst klasör olarak tutun **MyHelloWorld/WebContent**, aşağıda gösterildiği gibi:

   ![][ic659262]

1. İçinde **JSP şablon seç** iletişim kutusunda, Bu öğretici seçin amacıyla **yeni JSP dosyası (html)** tıklatıp **son**.

1. İndex.jsp dosyası Eclipse'te açıldığında, dinamik olarak görüntülenecek metni eklemek **Merhaba Dünya!** `<body>`Hello World! (Merhaba Dünya!) ifadesinin görüntülenmesi için metni ekleyin. Güncelleştirilmiş `<body>` içeriği aşağıdaki gibi görünmelidir:
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. İndex.jsp kaydedin.

## <a name="to-deploy-your-application-to-azure-the-quick-and-simple-way"></a>Uygulamanızı Azure, hızlı ve kolay şekilde dağıtmak için
Test etmek hazır bir Java web uygulamasına sahip olarak doğrudan Azure bulut üzerinde denemek için aşağıdaki kısayolu kullanabilirsiniz.

1. Eclipse'nın Proje Gezgini'nde tıklatın **MyHelloWorld**.

2. Eclipse araç çubuğunda **Yayımla** aşağı açılan düğme ve ardından **Azure bulut hizmeti olarak Yayımla**

   ![][publishDropdownButton]

3. Bu uygulamayı Azure'a ilk kez yayımlama ve önce bu uygulama için bir Azure dağıtım projesi oluşturmadıysanız, bir Azure dağıtım projesi sizin için otomatik olarak oluşturulması. Uygulamanızı çalıştırmak için otomatik olarak dağıtılacak uygulama sunucusu ve ayrıca JDK paketini listeler aşağıdaki istemi görmeniz gerekir.

   ![][ic789598]
   
   Bu kısayol yaklaşım belirli sunucu veya varsayılan adlardan farklı JDK yapılandırmak zorunda kalmadan Azure'da uygulamanızı test etmek hızlı ve kolay bir yol sağlar. Varsayılan değerlerle memnun kaldığınızda, tıklayabilirsiniz **Tamam** aşağıdaki adımlarla devam etmek için.
   Ancak, JDK değiştirmek istiyorsanız veya uygulama sunucusu, uygulamanız için kullanmak için bunu daha sonra sizin için otomatik olarak oluşturulan Azure dağıtım projesi düzenleyerek yapabilirsiniz veya tıklatabilirsiniz **iptal** şimdi ve okuma  **Azure dağıtım projeleri bölümü hakkında** Bu öğreticinin.

4. İçinde **Azure Yayımla** iletişim:

   1. Seçmek için hiçbir aboneliği varsa **abonelik** liste henüz abonelik bilgilerinizi içe aktarmak için aşağıdaki adımları izleyin:
      1. Tıklatın **yayımlama ayarları dosyasını içeri aktar**.
      2. İçinde **alma abonelik bilgilerini** iletişim kutusunda, tıklatın **yayımlama ayarları dosyası karşıdan**. Azure hesabınızda henüz tutulmaz, oturum açmak için istenir. Ardından Azure yayımlama ayarları dosyası istenir. Yerel makinenize kaydedin.
      3. Hala **alma abonelik bilgilerini** iletişim kutusunda, tıklatın **Gözat** düğmesi, yerel olarak önceki adımda kaydettiğiniz yayımlama ayarları dosyasını seçin ve ardından **açın**. Ekranınızın aşağıdakine benzer görünmelidir:![][ic644267]
      4. **Tamam** düğmesine tıklayın.
   2. İçin **abonelik**, dağıtımınız için kullanmak istediğiniz aboneliği seçin.
   3. İçin **depolama hesabı**, tıklayın veya kullanmak istediğiniz depolama hesabını seçin **yeni** yeni bir depolama hesabı oluşturmak için.
   4. İçin **hizmet adı**, tıklayın veya kullanmak istediğiniz bulut hizmeti seçin **yeni** yeni bir bulut hizmeti oluşturulamadı.
   5. İçin **hedef işletim sistemi**, dağıtımınız için kullanmak istediğiniz işletim sistemi sürümünü seçin.
   6. İçin **hedef ortam**, bu öğreticinin amaçları seçmek için **hazırlama**. (Üretim sitenize dağıtmaya hazır olduğunuzda, bu değiştireceğiz **üretim**.)
   7. İsteğe bağlı: emin **önceki dağıtım üzerine** yeni dağıtımınızı otomatik olarak önceki dağıtım üzerine yazmak isteyip istemediğinizi denetlenir. Bu seçeneği etkinleştirdiğinizde, aynı konuma yayımlarken değil deneyimi "409 çakışma" sorunlar olur.
      Unutmayın **Azure Yayımla** iletişim için bir bölüm içeren **uzaktan erişim**. Varsayılan olarak, uzaktan erişim etkin değildir ve biz, bu örnek için izin vermez. Uzaktan erişimi etkinleştirmek için bir kullanıcı adı ve uzaktan oturum açarken kullanılacak parolayı girmeniz gerekir. Uzaktan erişim hakkında daha fazla bilgi için bkz: [eclipse'te Azure dağıtımları için uzaktan erişim etkinleştirme][Enabling Remote Access for Azure Deployments in Eclipse].
      **Azure Yayımla** iletişim aşağıdakine benzer görünecektir:![][ic719488]

5. Tıklatın **Yayımla** hazırlama ortamına yayımlamak için.

   Tam bir yapı yapmak isteyip istemediğiniz sorulduğunda tıklatın **Evet**. Bu ilk derleme için birkaç dakika sürebilir.
   Bir **Azure etkinlik günlüğü** sekmeli Eclipse Görünümler bölümünde görüntülenir.
   ![][ic719489]Bu günlük kullanabilirsiniz yanı sıra **konsol** ilerleme dağıtımınızın durumunu görmek için görünümü. Oturum açmak için bir alternatif olan [Azure Yönetim Portalı][Azure Management Portal]ve **bulut Hizmetleri** durumunu izlemek için bölümü.

6. Dağıtımınız başarılı bir şekilde dağıtıldığında, **Azure etkinlik günlüğü** durumunu gösterecektir **yayımlanan**. Tıklatın **yayımlanan**aşağıdaki görüntüde gösterildiği gibi ve tarayıcınız dağıtımınızı örneğini açar.

   ![][ic719490]

Bu bir dağıtıma hazırlık ortamı olduğundan, DNS adı form http:// olacaktır&lt;*GUID*&gt;. cloudapp.net ve DNS adı ve uygulamanız için bir son eke içeren URL olacaktır. Örneğin, http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld. ( **MyHelloWorld** bölümü duyarlıdır.) Dağıtım adı (içinde Yönetim Portalı'nın bulut Hizmetleri kısmı) Azure platformu Yönetim Portalı'nda tıklatırsanız DNS adı de görebilirsiniz.

Bu kılavuz bir dağıtım için hazırlama ortamında olmasına rağmen üretim dağıtımına aynı adımları dışında içinde izleyen **Azure Yayımla** iletişim kutusunda **üretim** yerine **Hazırlama** için **hedef ortam**. Bir dağıtımı üretime hazırlama için kullanılan bir GUID yerine tercih ettiğiniz DNS adına göre bir URL ile sonuçlanır.

> [!WARNING]
> Bu noktada, Azure buluta dağıttınız. Ancak, devam etmeden önce çalışmadığı olsa bile, dağıtılan bir uygulama Faturalanabilir zaman aboneliğinize tahakkuk etmeye devam eder farkında olun. Bu nedenle, Azure aboneliğinizden istenmeyen dağıtımları silin son derece önemlidir.
> 
> 

## <a name="about-azure-deployment-projects"></a>Azure dağıtım projeleri hakkında
Bir veya daha fazla Java uygulamalarını azure'a dağıtmak için bir Azure dağıtım projesi gerekli değildir. "Uygulamalarınızı içine Azure üzerinde yayımlanması için sarmalamak gerek paketi" rol oynar.

Uygulamalarınızı hakkında bilgilerin yanı sıra, bir Azure dağıtım projesi hakkındaki bilgileri de diğer anahtar bileşenleri, dağıtımınızın en önemlisi içerir: web uygulamanızı çalıştırmak için uygulama sunucusu kapsayıcı ve çalıştırmak için Java Çalışma zamanı. Azure Java Çalışma zamanları ve Java uygulama sunucuları aralarından seçim yapabileceğiniz büyük seçimi destekler.

Burada kullanılan örnek eğitim amaçlı olarak büyük ölçüde basitleştirilmiş karşın, bir Azure dağıtım projesi neredeyse rasgele karmaşık, ölçeklenebilir, yüksek oranda kullanılabilir oluşturmanızı sağlayan diğer önemli yapılandırma bilgilerini de içerebilir, uygulamalarınızı çok katmanlı bulut hizmetleriyle. Etkinleştirebilirsiniz **oturum benzeşimi ("Yapışkan oturumları")**, **hızlı önbelleğe alma**, **SSL boşaltma**, **güvenlik duvarı/bağlantı noktası yönlendirme**, **uzaktan erişim**ve diğer güçlü özellikleri sayısı.

("Uygulamanızı Azure, hızlı ve kolay şekilde dağıtmak için") Bu öğreticinin önceki bölümde tamamladığınıza, sizin için otomatik olarak oluşturulur ve adlı proje Gezgini'nde yeni bir Azure dağıtım projesi şimdi görürsünüz " **MyHelloWorld_onAzure**".

Ayrıca bu öğreticinin ilk boş Azure dağıtım projesi kendiniz oluşturup ardından ona, uygulamaları ekleyerek başlattığınız. Bir uzun olduğundan işlem ancak başlangıçtan itibaren ilk yapılandırma üzerinde daha fazla denetim sağlar.

Sıfırdan yeni bir Azure dağıtım projesi oluşturmak için tıklatın **yeni Azure dağıtım projesi** düğmesini ![][ic710876].

Olup, zaten varolan bir Azure dağıtım projesi ile çalışma veya bir sıfırdan oluşturma bağımsız olarak, yapılandırma ayarlarını ve JDK veya uygulama sunucusu gibi bileşenleri eşit olarak değiştirebilmek için her zaman kolayca.

JDK veya uygulama sunucusu ya da var olan bir Azure dağıtım projesi uygulama listesinde değiştirmek için:

1. Proje düğümünü genişletin (örneğin **MyHelloWorld_onAzure**) proje Gezgini'nde

2. Sağ **WorkerRole1**

3. Genişletme **Azure** bağlam menüsünde alt

4. Tıklatın **sunucu yapılandırması**

Bakılmaksızın olup sunucu yapılandırma adımları yukarıda gösterildiği gibi mevcut bir Azure dağıtım projesi düzenleyerek başlattığınız ya da sıfırdan yeni bir tane oluşturmak, JDK, sunucu ve uygulama yapılandırmanıza olanak sağlayan iletişim kutuları aynı türde görürsünüz bileşenleri. Örneğin JDK, uygulama sunucusu değiştirmek ve eklemek veya bir dağıtımda, uygulamaları kaldırmak bu iletişim kutuları ayarları değiştirmek nasıl daha fazla bilgi için bkz: [sunucu yapılandırma özellikleri] [ Server configuration properties] makale.

## <a name="windows-only-to-deploy-your-application-to-the-compute-emulator"></a>Yalnızca Windows: işlem öykünücüsü uygulamanızı dağıtmak için

> [!NOTE]
> Yalnızca Windows Azure öykünücüsü kullanılabilir. Windows dışındaki bir işletim sistemi kullanıyorsanız, bu bölümü atlayabilirsiniz.
> 
> 

Daha önce yani örtük olarak açıklanan adımları izleyerek yeni bir Azure dağıtım projesi oluşturduysanız uygulamanızı Azure, JDK ve uygulama yayımlayarak sunucuları bulut ancak yerel öykünmesi için yapılandırılmış. Yerel öykünücüde test etmek için projenize hazırlamak için aşağıdaki adımları izleyin:

1. Eclipse'nın Proje Gezgini'nde tıklatın **MyHelloWorld_onAzure**.

2. Sağ **WorkerRole1**.

3. Genişletme **Azure** bağlam menüsünde alt.

4. Tıklatın **sunucu yapılandırması**.

5. Üzerinde **JDK** sekmesi, araç varsayılan önceden yapılandırılmış olmadığını denetleyin, yerel JDK. Değilse ya da kabul varsayılanları değiştirmek isterseniz, emin **yerel olarak test etmek için bu dosya yolundan JDK kullanmak** onay kutusu işaretli ve kullanmak istediğiniz JDK yükleme konumu belirtilir. Bunu değiştirmek istiyorsanız, tıklayın **Gözat** düğmesine tıklayın ve göz atma denetimi kullanarak, kullanılacak JDK dizin konumunu seçin.

6. Tıklatın **Server** sekmesi.

7. İçinde **yerel sunucu yolu** iletişim kutusunun altındaki metin kutusuna girin türü ve iletişim kutusunun üstündeki altında seçilen sunucu ana sürüm numarası eşleşen yerel olarak yüklenmiş bir sunucu yolu  **Bu tür bir sunucu dağıtımı** onay kutusu. Farklı tür veya uygulama sunucusu ana sürümüne kullanmak istiyorsanız, o onay kutusunu altında seçimi ilk değiştirin.

8. **Tamam** düğmesine tıklayın.

9. Eclipse araç çubuğunda **Azure öykünücüsünde çalıştırın** düğmesini ![][ic710879]. Varsa **Azure öykünücüsünde çalıştırın** düğmesi etkin değil, emin **MyHelloWorld_onAzure** Eclipse'nın Proje Gezgini'nde seçilir ve Eclipse'nın Proje Gezgini odak geçerli olarak sahip olduğundan emin olun penceresini açın. Bu ilk tam bir yapı projenizin başlatmak ve Java web uygulamanızı işlem öykünücüsü başlatın. (Bilgisayarınızın performans özellikleri, bağlı olarak ilk yapı birkaç dakika için birkaç saniye arasında alabilir, ancak sonraki oluşturur, Not daha hızlı alırsınız.) İlk derleme adımı tamamlandıktan sonra Windows kullanıcı hesabı denetimi (UAC) tarafından bilgisayarınıza değişiklik yapmak bu komutu izin istenir. **Evet**'e tıklayın.

> [!IMPORTANT]
> UAC istemi görmüyorsanız UAC simgesi için Windows görev çubuğunda denetleyin ve ilk'ı tıklatın. Bazen UAC istemi en üstteki bir pencere olarak görünmez, ancak yalnızca bir görev çubuğunda simge olarak görünür.
> 
> 

1. İşlem öykünücüsü, projenizin herhangi bir sorun olup olmadığını belirlemek için kullanıcı Arabirimi çıktıyı inceleyin. Dağıtımınızı içeriğini bağlı olarak, bu işlem öykünücüsü içinde tam olarak başlatılması, uygulamanız için birkaç dakika sürebilir.

2. Tarayıcınızı başlatın ve URL kullanmak `http://localhost:8080/MyHelloWorld` adresi olarak ( `MyHelloWorld` URL'sinin büyük küçük harfe duyarlı). MyHelloWorld uygulamanız (index.jsp çıkışını) görmeniz gerekir aşağıdaki görüntüde benzer:

   ![][ic589579]

Uygulamanızı Eclipse araç çubuğunda, işlem öykünücüsü'nde çalışmasını durdurmak hazır olduğunuzda tıklatın **Azure öykünücüsünü sıfırlayın** düğmesini ![][ic710880].

## <a name="to-delete-your-deployment"></a>Dağıtımınızı silmek için
Eclipse için Azure Araç Seti içinde dağıtımını silmek için emin olun **MyHelloWorld_onAzure** olan Eclipse'nın Proje Gezgini'nde seçili, Eclipse Proje Gezgini odaklanmanıza ve ardındangeçerlipencereyiolduğundaneminolun **Unpublish** düğmesini ![][ic710883], Eclipse araç. (Sağ tıklayarak aynı işlem yapabilirsiniz **MyHelloWorld_onAzure** tıklatarak Eclipse'nın Proje Gezgini'nde **Azure** ve ardından **Azure bulutaUndeploy**.) Bu görüntüler **yayımdan Azure projesi** iletişim.

![][ic719491]

Dağıtımınızı içerir abonelik ve bulut hizmeti seçin, silme ve ardından istediğiniz dağıtım **yayımdan**.

(Dağıtımını silmek için araç seti kullanarak kullanmaya alternatiftir **bulut Hizmetleri** Azure Yönetim Portalı bölümünde: dağıtımınıza gidin, onu seçin ve ardından **silme** düğme. Bu durdurmak ve ardından silin, dağıtım. Yalnızca dağıtım durdurmak istiyor ancak silemezsiniz, tıklatın **durdurmak** yerine düğmesini **silmek** düğmesi, ancak olarak belirtilen yukarıdaki dağıtım silmezseniz Faturalanabilir ücretleri devam edecek Dağıtımınız için tahakkuk) bile durdurulursa kullanılır.

## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse] 

[Eclipse için Azure Araç Seti yenilikleri][What's New in the Azure Toolkit for Eclipse]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

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
