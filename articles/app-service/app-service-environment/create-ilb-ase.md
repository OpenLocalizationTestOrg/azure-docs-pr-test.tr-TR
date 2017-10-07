---
title: "aaaCreate ve bir iç yük dengeleyici Azure uygulama hizmeti ortamı ile kullanma"
description: "Hakkında ayrıntılar toocreate ve bir internet yalıtılmış Azure uygulama hizmeti ortamı'nı kullanma"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a>Oluşturma ve bir iç yük dengeleyici ile uygulama hizmeti ortamı kullanma #

 Azure uygulama hizmeti ortamı bir Azure uygulama hizmeti dağıtımı bir Azure sanal ağındaki (VNet) bir alt ağ ile değil. Uygulama hizmeti ortamı (ana) iki yolu toodeploy vardır: 

- Dış IP adresi üzerinde bir VIP ile genellikle bir dış ana çağrılır.
- Bir iç yük dengeleyici (ILB) Hello iç uç nokta olduğu için bir iç IP adresinde bir VIP ile genellikle bir ILB ana çağrılır. 

Bu makale size nasıl gösterir toocreate bir ILB ana. Merhaba ana üzerinde bir genel bakış için bkz: [giriş tooApp hizmeti ortamları][Intro]. bir dış ana toocreate nasıl görürüm toolearn [bir dış ana oluşturma][MakeExternalASE].

## <a name="overview"></a>Genel Bakış ##

Bir ana internet'ten erişilebilen bir uç nokta veya bir IP adresi ile sanal ağınızda dağıtabilirsiniz. tooset başlangıç IP adresi tooa VNet adres, hello ana bir ILB ile dağıtılması gerekir. Bir ILB ile ana dağıttığınızda, sağlamanız gerekir:

-   Uygulamalarınızı oluştururken kullandığınız kendi etki alanı.
-   HTTPS için kullanılan hello sertifikası.
-   Etki alanınız için DNS yönetimi.

Buna karşılık, sizin gibi şeyler yapabilir:

-   İntranet uygulamalarını bulutta bir siteden siteye veya Azure ExpressRoute VPN aracılığıyla erişebileceğiniz güvenli bir şekilde hello, ana bilgisayar.
-   Genel DNS sunucuları listelenmeyen konak uygulamalar hello bulutta.
-   Ön uç uygulamalarınızı güvenli bir şekilde ile tümleştirebilirsiniz Internet yalıtılmış arka uç uygulamalar oluşturun.

### <a name="disabled-functionality"></a>Devre dışı bırakılan işlevsellik ###

Bir ILB ana kullandığınızda, bunu yapamazsınız bazı şeyler vardır:

-   IP tabanlı SSL kullanın.
-   IP adresleri toospecific uygulamaları atayın.
-   Satın alma ve hello Azure portal aracılığıyla bir uygulama ile bir sertifika kullanın. Doğrudan bir sertifika yetkilisinden sertifika almak ve bunları uygulamalarınızı ile kullanabilirsiniz. Bunları hello Azure portal elde edilemiyor.

## <a name="create-an-ilb-ase"></a>Bir ILB ana oluşturma ##

bir ILB ana toocreate:

1. Hello Azure portal, seçin **yeni** > **Web + mobil** > **uygulama hizmeti ortamı**.

2. Aboneliğinizi seçin.

3. Kaynak grubunu seçin veya oluşturun.

4. Bir VNet oluşturun veya seçin.

5. Varolan bir sanal ağ seçerseniz, bir alt ağ toohold hello ana toocreate gerekir. Tooset bir alt ağ boyutunu büyüklükte tooaccommodate gelecekteki büyümesine, ana emin olun. Dosya boyutu öneririz `/25`, 128 adresi olduğunu ve en büyük ölçekli bir ana işleyebilir. Merhaba minimum boyutu seçebileceğiniz bir `/28`. Altyapı gereken sonra bu boyut 11 örneklerinin ölçeklendirilmiş tooa en olabilir.

    * Uygulama hizmeti planlarında Hello varsayılan en fazla 100 örneklerinin gidin.

    * 100 yakın ancak daha hızlı ön uç ölçeklendirme ile ölçeklendirin.

6. Seçin **sanal ağ konumu** > **sanal ağ yapılandırması**. Set hello **VIP türü** çok**dahili**.

7. Bir etki alanı adı girin. Bu ana içinde oluşturulan uygulamaları için kullanılan hello bu etki alanıdır. Bazı kısıtlamalar vardır. Olamaz:

    * NET   

    * azurewebsites.NET

    * p.azurewebsites.NET

    * &lt;asename&gt;. p.azurewebsites.net

   Merhaba etki alanı adı, ana tarafından kullanılan çakışamaz ve uygulamalar için Hello özel etki alanı adı kullanılır. Bir ILB ana hello etki alanı adıyla için _contoso.com_, özel etki alanı adları gibi uygulamalar için kullanılamaz:

    * www.contoso.com

    * ABCD.def.contoso.com

    * ABCD.contoso.com

   Uygulamalarınız için hello özel etki alanı adlarını biliyorsanız, bu özel etki alanı adları ile bir çakışma olmaz ILB ana hello için bir etki alanı seçin. Bu örnekte, aşağıdakine benzer kullanabilirsiniz *contoso internal.com* , ana hello etki alanı için sonunda özel etki alanı adları ile çakışmaz çünkü *. contoso.com*.

8. Seçin **Tamam**ve ardından **oluşturma**.

    ![ASE oluşturma][1]

Merhaba üzerinde **sanal ağ** dikey penceresinde, var olan bir **sanal ağ yapılandırması** seçeneği. Bir dış VIP veya iç VIP tooselect kullanabilirsiniz. Merhaba varsayılandır **dış**. Seçerseniz **dış**, ana internet'ten erişilebilen bir VIP kullanır. Seçerseniz **iç**, ana sanal ağınızın içinde bir IP adresinde bir ILB ile yapılandırılır.

Siz seçtikten sonra **iç**, hello özelliği tooadd daha fazla IP adresleri tooyour ana kaldırılır. Bunun yerine, hello ana tooprovide hello etki alanı gerekir. ASE'de bir dış VIP ile hello hello ana adını hello etki alanında o ana oluşturulan uygulamalar için kullanılır.

Ayarlarsanız **VIP türü** çok**iç**, ana adınızı hello etki alanında ana hello için kullanılmaz. Merhaba etki alanını açıkça belirtin. Etki alanınız varsa *contoso.corp.net* ve ana adlı içeren bir uygulama oluşturmak *timereporting*, bu uygulama timereporting.contoso.corp.net için URL hello.


## <a name="create-an-app-in-an-ilb-ase"></a>ILB ASE'de bir uygulama oluşturun ##

ILB ASE'de hello bir uygulama oluşturun, bir uygulama ASE'de normalde oluşturmanızı aynı şekilde.

1. Hello Azure portal, seçin **yeni** > **Web + mobil** > **Web** veya **mobil** veya  **API uygulaması**.

2. Merhaba hello uygulama adını girin.

3. Merhaba aboneliği seçin.

4. Kaynak grubunu seçin veya oluşturun.

5. Bir uygulama hizmeti planı oluşturun veya seçin. Yeni bir uygulama hizmeti planı toocreate istiyorsanız, ana hello konumu olarak seçin. Oluşturulan, uygulama hizmeti planı toobe istediğiniz hello çalışan havuzu seçin. Merhaba uygulama hizmeti planı oluşturduğunuzda, ana hello konumu ve hello çalışan havuzu seçin. Merhaba uygulamasının hello adı belirttiğinizde, uygulama adı altında hello etki alanı için ana hello etki alanı tarafından değiştirilir.

6. **Oluştur**’u seçin. Panonuzda hello uygulama tooappear istiyorsanız seçin **PIN toodashboard** onay kutusu.

    ![Uygulama hizmeti planı oluşturma][2]

    Altında **uygulama adı**, hello etki alanı adıdır, ana güncelleştirilmiş tooreflect hello etki alanı.

## <a name="post-ilb-ase-creation-validation"></a>POST ILB ana oluşturma doğrulama ##

Bir ILB ana hello olmayan - ILB ana değerinden biraz farklıdır. Önceden belirtildiği gibi toomanage kendi DNS ihtiyacınız var. Ayrıca, kendi sertifika HTTPS bağlantıları için tooprovide vardır.

Hello etki alanı adı, ana oluşturduktan sonra belirttiğiniz hello etki alanı gösterir. Yeni bir öğe görünür **ayarı** adlı menüsü **ILB sertifika**. Merhaba ana hello ILB ana etki alanı belirtmeyen bir sertifika ile oluşturulur. Bu sertifika ile Merhaba ana kullanıyorsanız, tarayıcınızı geçersiz olduğunu söyler. Bu sertifika daha kolay tootest HTTPS kolaylaştırır, ancak bağlı tooyour ILB ana etki alanı kendi sertifikanızı tooupload gerekir. Bu adım sertifikanız veya otomatik olarak imzalanan bir sertifika yetkilisinden alınan bağımsız olarak gereklidir.

![ILB ana etki alanı adı][3]

ILB ana geçerli bir SSL sertifikası gerekir. İç sertifika yetkilileri kullanın, bir dış veren bir sertifika satın veya otomatik olarak imzalanan bir sertifika kullanın. Bağımsız olarak Hello kaynak hello SSL sertifikasının hello aşağıdaki sertifika öznitelikleri düzgün yapılandırılmış toobe gerekir:

* **Konu**: kök etki alanı burada too*.your bu özniteliği ayarlanmalıdır.
* **Konu alternatif adı**: Bu öznitelik her ikisini de içermelidir **kök etki alanı burada .your* ve **.scm.your-kök-etki-burada*. SSL bağlantıları toohello SCM/Kudu site her uygulamayla ilişkili hello formunun bir adres kullanın *your-app-name.scm.your-root-domain-here*.

Convert/hello SSL sertifikası bir .pfx dosyası olarak Kaydet. Hello .pfx dosyası, tüm ara içerir ve sertifikaları kök gerekir. Bir parola ile güvenli hale getirin.

Toocreate otomatik olarak imzalanan bir sertifika isterseniz, burayı hello PowerShell komutlarını kullanabilirsiniz. ILB ana etki alanı adınızı yerine emin toouse olması *internal.contoso.com*: 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

Merhaba sertifika tarayıcınızın güven zincirinde olan bir sertifika yetkilisi tarafından oluşturulmadıysa çünkü bu PowerShell komutlarını oluşturan hello sertifika tarayıcılar tarafından işaretlenir. tooget tarayıcınız güvenler, bir sertifika edinin, tarayıcınızın zincirinde güven, ticari sertifika yetkilisinden. 

![ILB sertifikayı ayarlayın][4]

tooupload kendi sertifikaları ve test erişim:

1. Merhaba ana oluşturulduktan sonra toohello ana UI gidin. Seçin **ana** > **ayarları** > **ILB sertifika**.

2. tooset hello ILB sertifika hello sertifika .pfx dosyasını seçin ve hello parolayı girin. Bu adım, bazı zaman tooprocess alır. Bir karşıya yükleme işlemi devam ediyor belirten bir ileti görüntülenir.

3. Merhaba ILB adresi için ana alırsınız. Seçin **ana** > **özellikleri** > **sanal IP adresi**.

4. Merhaba ana oluşturulduktan sonra ana bir web uygulaması oluşturun.

5. Bu VNet içinde yoksa, bir VM oluşturun.

    > [!NOTE] 
    > Bu VM toocreate denemeyin başarısız veya sorunlara neden olduğundan ana hello gibi aynı alt ağda hello.
    >
    >

6. Merhaba DNS ana etki alanınız için ayarlayın. DNS, etki alanı ile bir joker karakter kullanabilirsiniz. bazı basit toodo testleri, VM tooset hello web uygulaması adı toohello VIP IP adresi üzerinde hello hosts dosyasını düzenleyin:

    a. Merhaba etki alanı adı, ana sahipse, _. ilbase.com_ ve adlı hello web uygulaması oluşturma _mytestapp_, adresindeki ele _mytestapp.ilbase.com_. Ardından _mytestapp.ilbase.com_ tooresolve toohello ILB adresi. (Windows üzerinde hello hosts _C:\Windows\System32\drivers\etc dosyasıdır\_.)

    b. konsolunda, Gelişmiş tootest web dağıtımı yayımlama veya erişim toohello oluşturmak için bir kayıt _mytestapp.scm.ilbase.com_.

7. Bu VM üzerinde bir tarayıcı kullanın ve http://mytestapp.ilbase.com için gidin. (Veya web uygulaması adı, etki alanı ile olan toowhatever gidin.)

8. Bu VM üzerinde bir tarayıcı kullanın ve https://mytestapp.ilbase.com için gidin. Kendinden imzalı bir sertifika kullanıyorsanız, güvenlik hello eksikliği kabul edin.

    Başlangıç IP adresi, ILB için altında listelenen **IP adreslerini**. Bu liste hello dış VIP ve gelen yönetim trafiği için kullanılan hello IP adresleri de vardır.

    ![ILB IP adresi][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a>Web işleri, İşlevler ve ILB ana hello

Bir ILB ana işlevleri ve web işleri desteklenmektedir, ancak hello portal toowork için onlarla, ağ erişim toohello SCM site olması gerekir.  Bu, tarayıcınızı ya da kullanılıyor veya toohello sanal ağa bağlı bir konak üzerinde olması gerektiği anlamına gelir.  

Bir ILB ana Azure işlevleri kullandığınızda, "biz işlevlerinizi şu anda mümkün tooretrieve değildir. bildiren bir hata iletisi alabilirsiniz Lütfen daha sonra yeniden deneyin." Merhaba işlevleri UI hello SCM site HTTPS üzerinden yararlanır ve hello kök sertifikası hello tarayıcı zincirindeki güven olmadığından bu hata oluşur. Web işleri benzer bir sorun vardır. tooavoid bu sorunu hello aşağıdakilerden birini yapabilirsiniz:

- Merhaba sertifika tooyour güvenilen sertifika deposuna ekleyin. Bu sınır ve Internet Explorer kaldırır.
- Chrome kullanın ve ilk toohello SCM sitesine gidin, hello güvenilmeyen sertifikayı kabul ve toohello portal gidin.
- Güven, tarayıcı zincirindeki bir ticari sertifikası kullanın.  Merhaba en iyi seçenek budur.  

## <a name="dns-configuration"></a>DNS yapılandırması ##

Bir dış VIP kullandığınızda, DNS hello Azure tarafından yönetilir. Ana oluşturulan herhangi bir uygulama, Genel DNS olduğu tooAzure DNS, otomatik olarak eklenir. ILB ASE'de kendi DNS yönetmeniz gerekir. Gibi belirli bir etki alanının _contoso.net_, DNS A kayıtlarını DNS'e bu noktası tooyour ILB adresini toocreate gerekir:

- *. contoso.net
- *. scm.contoso.net

Bu ana dışında birden çok şey için ILB ana etki alanı kullandıysanız, toomanage DNS başına uygulamanızın-adı temelinde gerekebilir. Oluşturduğunuzda, tooadd her yeni uygulama adı, DNS gerektiği için bu yöntemi bir görevdir. Bu nedenle, ayrılmış bir etki alanı kullanmanızı öneririz.

## <a name="publish-with-an-ilb-ase"></a>Bir ILB ana ile yayımlama ##

Oluşturulan her uygulama için iki uç nokta vardır. ILB ASE'de elinizde  *&lt;uygulama adı >.&lt; ILB ana etki alanı >* ve  *&lt;uygulama adı > .scm.&lt; ILB ana etki alanı >*. 

Merhaba SCM site adını alır, hello adlı toohello Kudu konsol **Gelişmiş portal**, içinde Azure portal hello. Merhaba Kudu konsol, ortam değişkenleri görüntülemek, hello disk keşfetmek, bir konsol ve çok daha fazlasını kullanın sağlar. Daha fazla bilgi için bkz: [Kudu Konsolu Azure App Service için][Kudu]. 

Merhaba çok kullanıcılı uygulama hizmeti ve bir dış ana yoktur çoklu oturum açma hello Azure portal ve hello Kudu Konsolu arasında. Merhaba ILB ana ancak toouse yayımlama kimlik bilgileri toosign hello Kudu konsoluna gerekir.

Yayımlama Hello endpoint Internet erişilebilir olmadığı için Internet tabanlı CI sistemler, GitHub ve Visual Studio Team Services gibi bir ILB ana ile çalışmaz. Bunun yerine, toouse Dropbox gibi bir çekme modeli kullanan bir CI sistemi gerekir.

Yayımlama Hello uç noktaları bir ILB ana uygulamalar için ILB ana oluşturulması sırasında bu hello hello etki alanını kullanın. Bu etki alanı hello uygulamanın yayımlama profili ve hello uygulamanızın portal dikey penceresinde görünür (**genel bakış** > **Essentials** ve ayrıca **özellikleri**). Merhaba alt etki alanı ile bir ILB ana varsa *contoso.net* ve adlı bir uygulama *mytest*, kullanın *mytest.contoso.net* FTP ve *mytest.scm.contoso.net*  web dağıtımı için.

## <a name="couple-an-ilb-ase-with-a-waf-device"></a>Bir ILB ana WAF aygıt ile eşleştiği ##

Azure uygulama hizmeti hello sistemini koruma birçok güvenlik önlemleri sağlar. Bir uygulama ele olup olmadığını da toodetermine yardımcı olurlar. Merhaba en iyi bir web uygulaması için bir barındırma platformuyla, Azure uygulama hizmeti gibi bir web uygulaması Güvenlik Duvarı (WAF) toocouple korumadır. Merhaba ILB ana ağ yalıtılmış uygulama uç noktası olduğundan, bu tür bir kullanım için uygundur.

toolearn tooconfigure, ILB ana WAF aygıtla nasıl görürüm hakkında daha fazla [, uygulama hizmeti ortamınızı ile bir web uygulaması güvenlik duvarı yapılandırma][ASEWAF]. Bu makalede gösterilmektedir nasıl toouse Barracuda sanal gereç, ana ile. Toouse Azure uygulama ağ geçidi başka bir seçenektir. Uygulama ağ geçidi herhangi bir uygulama arkasında yerleştirilen hello OWASP çekirdek kuralları toosecure kullanır. Uygulama ağ geçidi hakkında daha fazla bilgi için bkz: [giriş toohello Azure web uygulaması güvenlik duvarı][AppGW].

## <a name="get-started"></a>başlarken ##

Tüm makaleler ve nasıl tooinstructions ASEs için kullanılabilir olan [uygulama hizmeti ortamları için Benioku][ASEReadme].

* ASEs ile başlatılan tooget bkz [giriş tooApp hizmeti ortamları][Intro].
* Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
