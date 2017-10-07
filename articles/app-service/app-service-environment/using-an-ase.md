---
title: "aaaUse Azure uygulama hizmeti ortamı"
description: "Nasıl toocreate, yayımlama ve uygulamaları Azure uygulama hizmeti ortamı ölçeklendirme"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 30c89e384efc07c560254856c0ca7d4eb4b1f010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-app-service-environment"></a>Bir uygulama hizmeti ortamı'nı kullanma #

## <a name="overview"></a>Genel Bakış ##

Azure uygulama hizmeti ortamı bir Azure uygulama hizmeti dağıtımı bir müşterinin Azure sanal ağındaki bir alt ağ ile değil. Aşağıdakilerden oluşur:

- **Ön Uçları**: hello ön uçlar olduğunuz nerede bir uygulama hizmeti ortamı'nda (ana) HTTP/HTTPS sonlandırır.
- **Çalışanlar**: hello çalışanlardır uygulamalarınızı barındırmak hello kaynakları.
- **Veritabanı**: hello veritabanı hello ortamı tanımlayan bilgileri tutar.
- **Depolama**: hello depolama olduğu kullanılan toohost hello müşteri yayımlanan uygulamalar.

> [!NOTE]
> Uygulama hizmeti ortamı iki sürümü vardır: ASEv1 ve ASEv2. ASEv1 içinde kullanabilmek için önce hello kaynakları yönetmeniz gerekir. toolearn nasıl tooconfigure ve ASEv1 yönetmek için bkz: [bir uygulama hizmeti ortamı v1 yapılandırma][ConfigureASEv1]. Merhaba, bu makalenin kalanında ASEv2 odaklanır.
>
>

Uygulama erişimi için bir harici veya dahili VIP ile bir ana (ASEv1 ve ASEv2) dağıtabilirsiniz. bir dış VIP ile Merhaba dağıtımı genellikle bir dış ana olarak adlandırılır. bir iç yük dengeleyici (ILB) kullandığından hello iç sürüm hello ILB ana adı verilir. toolearn hello ILB ana hakkında daha fazla bilgi görmek [oluşturma ve kullanma bir ILB ana][MakeILBASE].

## <a name="create-a-web-app-in-an-ase"></a>ASE'de bir web uygulaması oluşturma ##

toocreate bir ana web uygulamasında, ne zaman normalde oluşturmak, ancak bazı küçük farklar ile aynı işlemi hello kullanın. Yeni bir uygulama hizmeti planı oluşturduğunuzda:

- Uygulamanızın hangi toodeploy coğrafi bir konum seçmek yerine bir ana konumunuzu seçin.
- ASE'de oluşturulan tüm uygulama hizmeti planları, fiyatlandırma katmanı bir Isolated olması gerekir.

Bir ana yoksa, bir hello yönergeleri izleyerek oluşturabilirsiniz [uygulama hizmeti ortamı oluşturma][MakeExternalASE].

bir ana web uygulamasında toocreate:

1. Seçin **yeni** > **Web + mobil** > **Web uygulaması**.

2. Merhaba web uygulaması için bir ad girin. ASE'de zaten bir uygulama hizmeti planı seçtiyseniz hello uygulamasının hello etki alanı adı hello ana etki alanı adını hello yansıtır.

    ![Web uygulaması adı seçimi][1]

3. Bir abonelik seçin.

4. Yeni bir kaynak grubu için bir ad girin veya seçin **var olanı kullan** bir hello aşağı açılan listeden seçin.

5. Var olan bir uygulama hizmeti planı, ana seçin veya aşağıdaki adımları izleyerek yeni bir tane oluşturun:

    a. Seçin **Yeni Oluştur**.

    b. Uygulama hizmeti planınız için Hello adı girin.

    c. Ana hello seçin **konumu** aşağı açılan liste.

    d. Seçin bir **Isolated** fiyatlandırma katmanı. Seçin **seçin**.

    e. **Tamam**’ı seçin.
    
    ![Yalıtılmış fiyatlandırma katmanları][2]

6. **Oluştur**’u seçin.

## <a name="how-scale-works"></a>Nasıl çalışır ölçeklendirme ##

Her uygulama hizmeti uygulaması bir uygulama hizmeti planında çalışır. Merhaba kapsayıcı ortamları uygulama hizmeti planları basılı tutun ve uygulama hizmeti planları uygulamaları barındıracak modelidir. Bir uygulama ölçeklendirme, ölçeklendirme hello uygulama hizmeti planı ve böylece tüm hello uygulamalar hello ölçeklendirmek aynı planı.

Bir uygulama hizmeti planı ölçeklendirdiğinizde ASEv2 içinde gerekli hello altyapı otomatik olarak eklenir. Yoktur gecikme süresini tooscale işlemleri hello altyapı eklenirken. Oluşturma veya uygulama hizmeti planınızı ölçeklendirin önce ASEv1 içinde gerekli hello altyapı eklenmesi gerekir. 

Kaynak havuzu kullanıma hazır toosupport hello multitenant App Service, ölçekleme genellikle hemen olduğundan bu. Bir ana böyle bir arabellek yoktur ve kaynakları gerek ayrılır.

ASE'de, too100 örneği ölçeklendirebilirsiniz. Bu 100 örnekleri arasında birden çok uygulama hizmeti planları dağıtılmış veya tüm tek tek uygulama hizmeti planında olabilir.

## <a name="ip-addresses"></a>IP adresleri ##

Uygulama hizmeti hello özelliği tooallocate ayrılmış bir IP adresi tooan uygulama vardır. Bir IP tabanlı SSL yapılandırdıktan sonra bu özellik açıklandığı gibi kullanılabilir [bir var olan özel SSL sertifikası tooAzure web uygulamaları bağlamak][ConfigureSSL]. Ancak, ASE'de, önemli bir özel durum yoktur. Ek IP eklenemez bir ILB ana bir IP tabanlı SSL için kullanılan toobe yöneliktir.

Kullanabilmek için önce ASEv1 içinde tooallocate hello IP adreslerini kaynaklar olarak gerekir. Merhaba multitenant uygulama hizmeti gibi ASEv2, bunları uygulamanızdan kullanın. Her zaman bir yedek adres yok ASEv2 içinde too30 IP adresleri. Bir adresi her zaman kullanıma hazır olmasını sağlamak her birini kullanın, başka bir eklenir. Gecikme süresi tooallocate IP ekleme engelleyen başka bir IP adresi gerekli hızlı art arda adresleri.

## <a name="front-end-scaling"></a>Ön uç ölçeklendirme ##

Uygulama hizmeti planlarınızı ölçeklendirdiğinizde ASEv2 içinde çalışanları otomatik olarak toosupport eklenir bunları. Her ana iki ön uçlar ile oluşturulur. Ayrıca, hello ön uçlar otomatik olarak her 15 örnekleri için bir ön uç hızında uygulama hizmeti planlarında ölçeğini. 15 örneği varsa, örneğin, daha sonra üç ön uçlar sahip. Too30 örnekleri ölçeklendirme sonra dört ön uçları vb. varsa.

Ön Uçları sayısı fazlasıyla yeterlidir çoğu için senaryolar olmalıdır. Ancak, çıkışı daha hızlı bir oranda ölçeklendirebilirsiniz. Her beş örnekleri için bir ön uç olarak tooas düşük hello oranı değiştirebilirsiniz. Merhaba oranı değiştirmek bir ücret yoktur. Daha fazla bilgi için bkz: [Azure uygulama hizmeti fiyatlandırması][Pricing].

Merhaba HTTP/HTTPS uç noktası hello ana için ön uç kaynaklardır. Merhaba varsayılan ön uç yapılandırma ile ön uç başına bellek kullanımı sürekli olarak yaklaşık yüzde 60'tır. Müşteri iş yükleri bir ön uç üzerinde çalışmıyor. Merhaba anahtar saygı tooscale ile ön uç için öncelikle HTTPS trafiği tarafından yönlendirilen hello CPU faktördür.

## <a name="app-access"></a>Uygulama erişimi ##

Dış ASE'de uygulamaları oluştururken kullanılan hello etki alanı hello çok kullanıcılı App Service ' farklıdır. Merhaba ana hello adını içerir. Hakkında daha fazla bilgi için bkz toocreate bir dış ana [uygulama hizmeti ortamı oluşturma][MakeExternalASE]. bir dış ana Hello etki alanı adı arar gibi *.&lt; asename&gt;. p.azurewebsites.net*. Örneğin, ana adlı, _dış ana_ ve adlı bir uygulama ana bilgisayar _contoso_ o ana, bunu aşağıdaki URL'lere hello ulaşana:

- contoso.external ase.p.azurewebsites.net
- contoso.SCM.external ase.p.azurewebsites.net

Merhaba URL contoso.scm.external-ase.p.azurewebsites.net kullanılan tooaccess hello Kudu konsol ya da web kullanarak uygulamanızı yayımlama için dağıtın. Merhaba Kudu Konsolu hakkında daha fazla bilgi için bkz: [Kudu Konsolu Azure App Service için][Kudu]. Merhaba Kudu konsol, web kullanıcı Arabirimi sağlar hata ayıklama, dosyalar, dosyalar ve çok daha fazlasını düzenleme için.

ILB ASE'de dağıtım sırasında hello etki alanı belirler. Toocreate bir ILB ana, nasıl görürüm hakkında daha fazla bilgi için [oluşturma ve kullanma bir ILB ana][MakeILBASE]. Merhaba etki alanı adı belirtirseniz, _ılb ase.info_, ana kullanın, bu etki alanı app oluşturma sırasında uygulamaları hello. Adlı hello uygulama için _contoso_, hello URL'ler:

- contoso.ilb ase.info
- contoso.SCM.ilb ase.info

## <a name="publishing"></a>Yayımlama ##

Merhaba çok kullanıcılı olarak App Service ile ASE'de ile yayımlayabilirsiniz:

- Web dağıtımı.
- FTP.
- Sürekli Tümleştirme.
- Merhaba Kudu konsolunda sürükleyip yeniden açın.
- Visual Studio, Eclipse ya da Intellij Idea gibi bir IDE.

Bir dış ana ile tüm davranır Bu yayımlama seçeneklerini aynı hello. Daha fazla bilgi için bkz: [Azure App Service'te dağıtım][AppDeploy]. 

Yayımlama Hello önemli fark saygı tooan ILB ana ' dir. Bir ILB ana ile yayımlama hello uç noktalar yalnızca hello ILB tüm büyük/küçük harf kullanılabilir. Merhaba ILB özel IP hello ana alt hello sanal ağında açıktır. Ağ erişim toohello ILB yoksa, o ana tüm uygulamaların yayımlanamıyor. İçinde belirtildiği gibi [oluşturma ve kullanma bir ILB ana][MakeILBASE], tooconfigure DNS hello sistemde hello uygulamaları için gerekir. Merhaba SCM uç noktasının dahildir. Bunlar düzgün tanımlanmamış, yayımlanamıyor. IDE toohave ağ erişim toohello ILB sipariş toopublish etmeniz doğrudan tooit.

Yayımlama Hello endpoint Internet erişilebilir olmadığı için Internet tabanlı CI sistemler, GitHub ve Visual Studio Team Services gibi bir ILB ana ile çalışmaz. Bunun yerine, toouse Dropbox gibi bir çekme modeli kullanan bir CI sistemi gerekir.

Yayımlama Hello uç noktaları bir ILB ana uygulamalar için ILB ana oluşturulması sırasında bu hello hello etki alanını kullanın. Merhaba uygulamanın yayımlama profili ve hello uygulamanızın portal dikey görebilirsiniz (içinde **genel bakış** > **Essentials** ve ayrıca **özellikleri**). 

## <a name="pricing"></a>Fiyatlandırma ##

adlı SKU fiyatlandırma hello **Isolated** yalnızca ASEv2 ile kullanmak için oluşturuldu. Tüm ASEv2 içinde barındırılan uygulama hizmeti planları, SKU fiyatlandırma Isolated hello. Yalıtılmış uygulama hizmeti planı hızları, bölge başına farklılık gösterebilir. 

Ayrıca uygulama hizmetiniz için toohello fiyatı planları, ana kendisi için bir düz oranı. Merhaba düz oranı, ana hello boyutuyla değiştirmez ve 1 ek oranını ölçeklendirme varsayılan hello ana altyapısının için ödenen her 15 uygulama hizmeti planı örnekleri için ön uç.  

Merhaba varsayılan ölçek oranı 1 ön uç her 15 uygulama hizmeti planı örnekleri için yeterince hızlı değilse, ön uç eklenir veya hello ön uç boyutunu hello hello oranı ayarlayabilirsiniz.  Merhaba oranı veya boyutunu ayarladığınızda, varsayılan olarak ekleneceği değil hello ön uç çekirdekleri ücret ödersiniz.  

Örneğin, bir ön uç hello ölçek oranı too10 ayarlarsanız, her 10 örnekleri için uygulama hizmeti planları eklenir. Merhaba ücret her 15 örnekleri için bir ön uç ölçek oranını kapsar. 10 ölçek oranını ile Merhaba 10 uygulama hizmeti plan örneği eklediği hello üçüncü ön uç için ücret ödersiniz. Otomatik olarak eklendiğinden 15 örnekleri ulaştığında toopay için gerekmez.

Merhaba ön uç too2 çekirdek hello boyutunu ayarlanmış, ancak için ödeme sonra hello oranı ayarlama ek çekirdek hello.  Bir ana 2 ön uç, hello boyutu too2 çekirdek ön uç artan varsa ek 2 Çekirdek için ödeme böylece bile hello otomatik ölçeklendirme eşiğin altına oluşturulur.

Daha fazla bilgi için bkz: [Azure uygulama hizmeti fiyatlandırması][Pricing].

## <a name="delete-an-ase"></a>Bir ana Sil ##

bir ana toodelete: 

1. Kullanım **silmek** hello hello üstündeki **uygulama hizmeti ortamı** dikey. 

2. Toodelete istediğiniz, ana tooconfirm Hello adını girin. Bir ana sildiğinizde, tüm içeriğini hello içindeki da silersiniz. 

    ![Ana silme][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


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
