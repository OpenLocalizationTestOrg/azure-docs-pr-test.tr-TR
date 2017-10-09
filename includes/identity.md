Kimlik Yönetimi şirket içinde olduğu gibi hello genel bulutta önemli olduğu. toohelp bu Azure birkaç farklı bulut kimlik teknolojilerini destekler. Bu ayarlar şunlardır:

* Windows Server Active (yalnızca AD olarak bilinir) Directory hello bulut Azure sanal makineler ile oluşturulan sanal makineleri kullanarak çalıştırabilirsiniz. Azure tooextend kullanırken bu yaklaşım, şirket içi veri merkezi hello bulutunu mantıklıdır.
* Kullanıcılarınız tek oturum açma çok Azure Active Directory toogive kullanabileceğiniz[(SaaS) hizmet olarak yazılım](https://azure.microsoft.com/overview/what-is-saas/) uygulamalar. Örneğin, Microsoft Office 365 bu teknolojisini kullanır ve Azure veya Bulut platformlarıyla üzerinde çalışan uygulamalar de kullanabilirsiniz.
* Hello çalışan uygulamalar Bulut veya şirket içi Azure Active Directory erişim toolet kullanıcıların Facebook, Google, Microsoft ve diğer kimlik sağlayıcılardan kimliklerden kullanarak oturum açma denetimi kullanabilirsiniz.

Bu makalede bu seçeneklerin üçünü açıklanmaktadır.

## <a name="table-of-contents"></a>İçindekiler
* [Windows Server Active Directory sanal makinelerde çalışan](#adinvm)
* [Azure Active Directory'yi kullanma](#ad)
* [Azure Active Directory erişim denetimi kullanma](#ac)

## <a name="adinvm"></a>Windows Server Active Directory sanal makinelerde çalışan
Windows Server AD Azure sanal makinelerinde şirket içi çalışan benzer çalışıyor. [Şekil 1](#fig1) bu sistem, tipik bir örneği gösterir.

![Sanal makine Azure Active Directory'de](./media/identity/identity_01_ADinVM.png)

<a name="Fig1"></a>Şekil 1: Windows Server Active Directory Azure sanal ağını kullanarak bağlı Azure sanal makineleri tooan kuruluşun şirket içi veri merkezinde çalıştırabilirsiniz.

Burada gösterilen hello örnekte, Windows Server AD Azure sanal makineler, hello platformun Iaas teknolojisi kullanılarak oluşturulan VM çalışıyor. Bu sanal makineleri ve diğer birkaç Azure sanal ağı kullanan bir sanal ağa bağlı tooan şirket içi veri merkezine gruplandırılır. bir grup bulut sanal makinelerin, sanal özel ağ (VPN) bağlantısı üzerinden hello şirket içi ağ etkileşimde çıkışı Hello sanal ağ yontar. Bu sağlar yapmak bu Azure sanal makineleri başka bir alt ağ toohello şirket içi veri merkezi gibi görünüyor. Merhaba şekil gösterildiği gibi iki bu VM'lerin Windows Server AD etki alanı denetleyicileri çalışıyor. Merhaba hello sanal ağındaki diğer sanal makineler, SharePoint veya bazı diğer yolla gibi geliştirme ve test için kullanılan gibi uygulamaları çalışıyor olabilir. Merhaba şirket içi veri merkezi, iki Windows Server AD etki alanı denetleyicisi de çalışıyor.

Çalıştıran şirket içi olanla hello bulutta bağlanan hello etki alanı denetleyicileri için birkaç seçenek vardır:

* Bunların tümünün olun tek bir Active Directory etki alanının parçası.
* Ayrı AD etki alanları şirket içi oluşturmak ve hello parçası olan hello bulutta aynı orman.
* Merhaba Bulut ve şirket içi ayrı AD ormanına oluşturun, ardından ormanlar arası güven veya Windows Server Active Directory Federasyon, sanal makineleri Azure üzerinde de çalıştırabilirsiniz Hizmetleri (AD FS) kullanarak hello ormanlar bağlayın.

Hangi seçim yapıldığında, bir yönetici hello bağlantı toohello bulut büyük olasılıkla toobe şirket içi ağlarda yavaş olduğundan toocloud etki alanı denetleyicileri yalnızca gerekli olduğunda, şirket içi kullanıcıların kimlik doğrulama isteklerini Git emin olmanız gerekir. Başka bir faktör tooconsider bağlanan Bulut ve şirket içi etki alanı denetleyicileri, çoğaltma tarafından üretilen hello trafiğidir. Etki alanı denetleyicileri hello bulutta genellikle çoğaltma yapılır bir yönetici tooschedule ne sıklıkta veren kendi AD sitede etkilenir. Azure veri merkezi dışında için hangi hello yöneticinin çoğaltma seçenekleri etkileyebilir, gönderilen bayt değil ancak gönderilen trafiğin Azure ücretlerine uygulanabilir. Ayrıca Azure kendi etki alanı adı sistemi (DNS) destek sağlamasına karşın, bu hizmet (örneğin, dinamik DNS SRV kayıtları için destek) Active Directory tarafından gerekli özellikleri eksik işaret eden değer değildir. Bu nedenle, Windows Server AD Azure üzerinde çalışan kendi DNS sunucularınızı hello bulutta oluşturulması gerekir.

Windows Server AD Azure Vm'lerde çalışan birkaç farklı durumlarda mantıklı. İşte bazı örnekler:

* Azure sanal makineleri, kendi veri merkezinizin uzantı olarak kullanıyorsanız, Windows tümleşik kimlik doğrulaması istekleri ya da LDAP sorguları gibi yerel etki alanı denetleyicileri toohandle ayar yapmanız gerekir hello bulutta uygulamaları çalıştırabilirsiniz. SharePoint, örneğin, sık Active Directory ile etkileşim kurar ve olası toorun bir şirket içi dizin kullanarak azure'da bir SharePoint grubu olmakla birlikte, bu nedenle etki alanı denetleyicileri hello bulutta ayarlama önemli ölçüde performansı iyileştirir. (Ancak bu mutlaka gerekli değildir, önemli toorealize olduğu; yeterince uygulamaların yalnızca şirket içi etki alanı denetleyicilerini kullanarak hello bulutta başarılı bir şekilde çalıştırabilirsiniz.)
* Bir uzak şube ofisi hello kaynakları toorun kendi etki alanı denetleyicileri eksik varsayalım. Bugün, kullanıcılarına diğer tarafını hello world hello toodomain denetleyicilerinde kimliğini doğrulaması gerekir - oturumlardır yavaş. Active Directory yakın Microsoft Veri merkezinde Azure üzerinde çalışan bu hello şube ofisindeki daha fazla sunucu gerektirmeden hızlandırma.
* Olağanüstü durum kurtarma için Azure kullanan bir kuruluşun bir etki alanı denetleyicisi de dahil olmak üzere hello bulutta etkin VM'ler, küçük bir kümesini koruyabilir. Ardından olabilir tooexpand bu site gerekli tootake üzerinden başka bir yerde hataları için hazır.

Diğer olasılık vardır. Örneğin, gerekli etmediğinizden tooconnect hello bulut tooan Windows Server'da AD şirket içi veri merkezi. Toorun belirli bir kullanıcı kümesini sunulan bir SharePoint grubu istediyseniz, örneği için tüm KB'ye yalnızca bulut tabanlı kimliklerle oturum, Azure üzerinde bir tek başına orman oluşturabilirsiniz. Bu teknoloji kullanma hedefleriniz nelerdir bağlıdır. (Daha ayrıntılı Azure ile Windows Server AD kullanma konusunda yönergeler için [Burada gördüğünüz](http://msdn.microsoft.com/library/windowsazure/jj156090.aspx).)

## <a name="ad"></a>Azure Active Directory'yi kullanma
SaaS uygulamaları ve daha yaygın hale geldikçe bunlar belirgin bir soru Yükselt: ne tür bir dizin hizmeti bu bulut tabanlı uygulamalar kullanmalısınız? Microsoft'un yanıt toothat soru Azure Active Directory ' dir.

Bu dizin hizmeti hello bulutta kullanmak için iki ana seçeneğiniz vardır:

* Azure Active Directory, kişiler ve yalnızca SaaS uygulamaları kullanan kuruluşlar kendi tek dizin hizmeti güvenebilirsiniz.
* Windows Server Active Directory çalıştırmak kuruluşlar kendi şirket içi dizin tooAzure Active Directory connect sonra toogive kullanın, kullanıcılar tek oturum açma tooSaaS uygulamalar.

[Şekil 2](#fig2) hello gösterilmektedir ilk Azure Active Directory olduğu gerekli olan tüm bu iki seçenekten biri.

![Sanal makine Azure Active Directory'de](./media/identity/identity_02_AD.png)

<a name="fig2"></a>Şekil 2: Azure Active Directory kuruluşun kullanıcılar Office 365 dahil olmak üzere çoklu oturum açma tooSaaS uygulamalarını sağlar.

Merhaba şekil gösterildiği gibi Azure AD çok kiracılı bir hizmettir. Bu, kullanıcıların her biri hakkında dizin bilgilerini depolamak birçok farklı Kuruluş aynı anda destekleyebileceği anlamına gelir. Bu örnekte, bir kuruluştaki kullanıcı tooaccess bir SaaS uygulaması çalışıyor. Bu uygulama, SharePoint Online gibi Office 365 parçası olabilir veya başka bir şey olabilir - Microsoft dışı uygulamalar bu teknolojiyi de kullanabilirsiniz. Azure AD hello SAML 2.0 protokolü desteklediğinden, tüm bir uygulamadan bu endüstri standardı hello özelliği toointeract kullanarak istedi. (Aslında, Azure AD kullanan uygulamaların herhangi veri merkezinde, yalnızca Azure veri merkezinde çalıştırabilirsiniz.)

Merhaba kullanıcı bir SaaS uygulaması (1. adım) eriştiğinde hello işlemi başlar. toouse bu uygulama, Azure AD tarafından verilmiş bir belirteç hello kullanıcının sunması gerekir.

Bu belirteç hello kullanıcı tanımlayan bilgiler içerir ve Azure AD tarafından dijital olarak imzalanır. tooget hello belirteci hello kullanıcı kendisi tooAzure AD bir kullanıcı adı ve parola (2. adım) sağlayarak kimliğini doğrular. Ardından Azure AD pastaya ihtiyacı hello belirteci döndürür (3. adım).

Bu belirteç hello belirtecin imzayı doğrular ve içeriğini (5. adım) kullanan toohello SaaS uygulaması (4. adım), sonra gönderilir. Merhaba uygulaması hello belirteç hangi bilgi hello kullanıcı tooaccess izin toodecide içerir hello kimlik bilgileri genellikle, kullanır ve diğer yollarla belki de.

Merhaba uygulaması hello kullanıcı hakkında daha fazla bilgi hello belirtecinde yer alan daha gerekiyorsa, bunu doğrudan hello Azure AD Graph API (6. adım) kullanarak Azure AD'den isteyebilir. Merhaba ilk sürümünde Azure AD, hello directory şeması oldukça basittir: yalnızca kullanıcılar ve gruplar ve aralarındaki ilişkiler içerir. Uygulamalar, bu kullanıcılar arasında bağlantılar hakkında bilgi toolearn kullanabilir. Örneğin, uygulamanın kendisinin izin verilen erişim toosome veri yığınını olup toodecide bu kullanıcının yöneticisi olan tooknow gerektiğini varsayalım. Bu, Azure AD grafik API'si hello üzerinden sorgulayarak öğrenebilirsiniz.

Merhaba grafik API'si mobil cihazlar dahil olmak üzere çoğu istemcilerden basit toouse olmasını sağlayan bir sıradan RESTful protokolünü kullanır. Merhaba API OData, bir sorgu dili toolet istemcileri erişim verileri gibi şeyler daha kullanışlı şekilde ekleme tarafından tanımlanan hello uzantıları da destekler. (OData hakkında daha fazla bilgi için bkz: [Tanıtımı OData](http://download.microsoft.com/download/E/5/A/E5A59052-EE48-4D64-897B-5F7C608165B8/IntroducingOData.pdf).) Merhaba grafik API'si kullanıcılar arasında ilişkiler hakkında kullanılan toolearn olabileceğinden, uygulamaları (Merhaba grafik API'si adlı neden olan) belirli bir kuruluş için hello Azure AD şemada katıştırılmış hello sosyal grafik anlamanıza olanak sağlar. Ve tooauthenticate kendisini tooAzure AD grafik API'si için istekleri, uygulama OAuth 2.0 kullanan.

Bir kuruluş Windows Server Active Directory kullanmayan - şirket içi sunucu ya da etki alanları - sahip ve Azure AD kullanan yalnızca bulut uygulamaları kullanır, yalnızca bu bulut dizini kullanarak hello firmasının kullanıcılar tek oturum açma tooall bunların verirsiniz. Henüz bu senaryoda her gün daha yaygın alır, ancak çoğu kuruluş hala kullanım Windows Server Active Directory ile oluşturulan etki alanları şirket içi. Azure AD sahip yararlı rol tooplay burada de olarak [Şekil 3](#fig3) gösterir.

![Sanal makine Azure Active Directory'de](./media/identity/identity_03_AD.png)
<a id="fig3"></a>Şekil 3: bir kuruluş Windows Server Active Directory Kullanıcıları tek oturum açma tooSaaS uygulamaları ile Azure Active Directory toogive devredebilir.

Bu senaryoda, kuruluştaki B bir kullanıcı bir SaaS uygulaması tooaccess istiyor. Bunu yapmadan önce hello kuruluşunuzun dizin yöneticileri hello şekil gösterildiği gibi AD FS kullanarak Azure AD ile bir Federasyon ilişkisi oluşturmanız gerekir. Bu yöneticileri hello kuruluşun şirket içi Windows Server AD ve Azure AD arasında veri eşitlemeye de yapılandırmanız gerekir. Bu otomatik olarak kullanıcı ve grup bilgileri hello şirket içi dizin tooAzure AD kopyalar. Bu sağlar dikkat edin: etkin, hello kuruluşun kendi şirket içi dizin hello buluta genişletilmesi. Windows Server AD ve bu şekilde Azure AD birleştirme hello kuruluş tek bir varlık olarak bir boyut her iki şirket içi yaşamaya sırasında ve hello bulutta yönetilen bir dizin hizmeti sağlar.

Azure AD toouse hello kullanıcı ilk tooher şirket içi Active Directory etki alanında her zamanki gibi (1. adım) günlüğe yazar. Hello Federasyon işlemi, aynen tooaccess Merhaba SaaS uygulaması (2. adım) çalıştığında, her (adım 3) bu uygulama için bir belirteç veren Azure AD sonuçlanır. (Federasyon nasıl çalıştığı hakkında daha fazla bilgi için bkz: [Windows için talep tabanlı kimlik: teknolojileri ve senaryolar](http://www.davidchappell.com/writing/white_papers/Claims-Based_Identity_for_Windows_v3.0--Chappell.docx).) Önce bu belirteç bilgileri içerdiğinden hello kullanıcı tanımlar ve Azure AD tarafından dijital olarak imzalanır. Bu belirteç hello belirtecin imzayı doğrular ve içeriğini (5. adım) kullanan toohello SaaS uygulaması (4. adım), sonra gönderilir. Ve hello önceki senaryoda, SaaS uygulama kullanabilir, grafik API'si toolearn Bu kullanıcıyla ilgili daha fazla hello hello gerekli (adım 6).

Bugün, Azure AD şirket içi Windows Server AD için tam yenileme değil. Zaten söz edildiği gibi bir çok daha basit bir şema hello bulut dizine sahip ve Grup İlkesi, makine ve LDAP desteği hakkında hello özelliği toostore bilgi gibi şeyler eksik. (Aslında, bir Windows makinesine Azure AD ancak hiçbir şey kullanarak tooit kullanıcılar oturum yapılandırılmış toolet olamaz - bu desteklenen bir senaryo değildir.) Bunun yerine, ayrı bir oturum açma korumadan Kurumsal kullanıcıların erişim hello bulut uygulamalarında izin vererek hello ilk Azure AD amaçları içerir ve boşaltma el ile kendi şirket içi dizin ile eşitlenmesini directory yöneticileri şirket içi Her SaaS uygulaması kuruluşu kullanır. Zamanla, ancak, bu bulut dizin hizmeti tooaddress geniş bir senaryo bekler.

## <a name="ac"></a>Azure Active Directory erişim denetimi kullanma
Bulut tabanlı kimlik teknolojileri kullanılan toosolve çeşitli sorunlar olabilir. Azure Active Directory bir kuruluşun kullanıcı oturum açma tek toomultiple SaaS uygulamaları, örneğin verebilirsiniz. Ancak, diğer yollarla hello bulut kimlik teknolojileri de kullanılabilir.

Örneğin, bir uygulama kullanıcılarının oturum birden çok tarafından yayınlanan belirteçleri kullanarak toolet istediği düşünelim *kimlik sağlayıcıları (IdPs)*. Facebook, Google, Microsoft ve diğerleri de dahil olmak üzere çok sayıda farklı kimlik sağlayıcıları Günümüzde, mevcut ve uygulamaları sık bu kimlikleri birini kullanarak oturum açmalarına olanak tanır. Bunun yerine zaten kimlikleri üzerinde güvenebilirsiniz zaman neden bir uygulama toomaintain kullanıcılar ve parolalar kendi listesi rahatsız? Varolan kimlikleri kabul ömrü hem kullanıcı adları ve parolalar kendi listeleri artık toomaintain gereksinim duyan Merhaba uygulaması oluşturma hello kişilere ve bir kullanıcı adı ve parola tooremember daha az sahip kullanıcılar için basitleştirir.

Ancak belirteç çeşit her kimlik sağlayıcısı sorunları olsa da, bu belirteçleri standart olmayan - her IDP kendi biçimdedir. Ayrıca, bu belirteçleri hello bilgileri de standart değil. Bir söyleyin tarafından yayınlanan tooaccept belirteçleri isteyen uygulama, Facebook, Google ve Microsoft bu farklı biçimlerden her biri benzersiz bir kod toohandle yazma hello sınama ile karşılaştığı.

Ancak bunun neden? Neden kimlik bilgilerini ortak bir gösterimi olan tek bir belirteci biçimi oluşturabilen bir aracı yerine oluşturulsun mu? Bu yaklaşım ömrü daha basit uygulamaları, artık belirtecin yalnızca bir tür toohandle gerektiğinden oluşturan hello geliştiriciler için hale getirir. Azure Active Directory erişim denetimi tam olarak bunu çeşitli belirteçleri ile çalışmak için bir aracı hello bulutta sağlama yapar. [Şekil 4](#fig4) nasıl çalıştığını gösterir

![Sanal makine Azure Active Directory'de](./media/identity/identity_04_IdentityProviders.png)
<a id="fig4"></a>Şekil 4: Azure Active Directory erişim denetimi için farklı kimlik sağlayıcılar tarafından yayınlanan uygulamaları tooaccept kimlik belirteçlerini kolaylaştırır.

bir kullanıcı bir tarayıcıdan tooaccess Merhaba uygulaması çalıştığında hello işlemi başlar. Merhaba uygulaması kendi tooan kendi seçtikleri IDP yönlendirir (ve bu Merhaba uygulaması da güvenleri). Aynen kendisini toothis IDP, gibi bir kullanıcı adı ve parola (1. adım) girerek kimliğini doğrular ve kendi (2. adım) hakkında bilgi içeren bir belirteç hello IDP döndürür.

Erişim denetimi Hello şekil gösterildiği gibi Google, Yahoo, Facebook, (önceki adıyla Windows Live ID olarak da bilinir) Microsoft ve Openıd sağlayıcısı tarafından oluşturulan hesapların dahil farklı bulut tabanlı IdPs aralığını destekler. Azure Active Directory kullanılarak oluşturulan kimlikleri de destekler ve AD FS, Windows Server Active Directory ile Federasyon aracılığıyla. Merhaba Bulut veya şirket içi IdPs tarafından verilen hello toocover en yaygın olarak kullanılan hello kimlikleri bugün hedeftir.

Merhaba kullanıcının tarayıcısının kendi seçilen IDP IDP belirtece sonra bu gönderir tooAccess denetimi (3. adım) belirteci. Erişim denetimi, gerçekten bu IDP tarafından verilmiş, ardından bu uygulama için tanımlanmış toohello kurallarına göre yeni bir belirteç oluşturur, emin hello belirteci doğrular. Azure Active Directory gibi erişim denetimi çok kiracılı bir hizmet, ancak hello kiracılar müşteri kuruluşlar yerine uygulamalar. Her uygulamanın kendi ad alanı hello şekil gösterildiği gibi alabilir ve yetkilendirme ve daha fazlası hakkında çeşitli kurallar tanımlayabilirsiniz.

Bu kurallar, çeşitli IdPs gelen belirteçleri bir erişim denetimi belirtecine nasıl dönüştürülmesi gereken tanımlamak her uygulamanın yönetici olanak tanır. Örneğin, kullanıcı adlarını temsil etmek için farklı farklı IdPs kullanırsanız, erişim denetimi kuralları tüm ortak bir kullanıcı adı türü içine bunların dönüştürebilirsiniz. Erişim denetimi toohello uygulama (5. adım) gönderdiği bu yeni belirteci geri toohello tarayıcısı (4. adım), ardından gönderir. Merhaba erişim denetimi belirtecine sahip sonra Merhaba uygulaması bu belirteç gerçekten erişim denetimi tarafından verilmiş, sonra (adım 6) içerdiği hello bilgileri kullanır, doğrular.

Bu işlem biraz karmaşık görünebilir, ancak gerçekte yaşam hello oluşturan Merhaba uygulaması için önemli ölçüde daha basit kolaylaştırır. Farklı bilgi içeren çeşitli belirteçleri işlemek yerine hello uygulama hala tek belirteciyle tanıdık bilgi alırken birden çok kimlik sağlayıcılar tarafından yayınlanan kimlikleri kabul edebilir. Ayrıca, her uygulama toobe tootrust çeşitli IdPs yapılandırılmış gerektiren yerine bu güven ilişkileri yerine erişim denetimi tarafından korunur - uygulamanın yalnızca buna güvenmesi.

İşaret eden bağlı tooWindows erişim denetimi hakkında doğrudur - yalnızca Google ve Facebook kimlikleri kabul Linux uygulama tarafından da kullanılabilir değer olduğu. Ve erişim denetimi hello Azure Active Directory ailesinin bir parçası olsa bile, bunu ne hello önceki bölümde açıklandığı gelen tamamen ayrı bir hizmet olarak düşünebilirsiniz. Her iki teknolojinin kimliği ile çalışırken (Microsoft bu noktada toointegrate hello iki bekliyor denirse olsa da) oldukça farklı sorunları ele.

Neredeyse her uygulama kimliği ile çalışma önemlidir. Merhaba erişim denetimi hedefidir toomake kimlik bilgilerinden farklı kimlik sağlayıcıları kabul geliştiriciler toocreate uygulamalar için daha kolaydır. Bu hizmet hello bulutta koyarak, Microsoft, herhangi bir platformda çalışan kullanılabilir tooany uygulama sağlamıştır.

## <a name="about-hello-author"></a>Merhaba Yazar hakkında
David Chappell olduğundan, asıl Chappell & ilişkilendirilmiş bir [www.davidchappell.com](http://www.davidchappell.com) San Francisco, California.

