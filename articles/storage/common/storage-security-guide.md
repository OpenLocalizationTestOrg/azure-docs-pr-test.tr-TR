---
title: "aaaAzure depolama Güvenlik Kılavuzu | Microsoft Docs"
description: "Ayrıntılar bunlarla sınırlı tooRBAC, depolama hizmeti şifrelemesi, istemci tarafı şifreleme, SMB 3.0 ve Azure Disk şifrelemesi dahil olmak üzere Azure Storage, güvenlik altına almanın birçok yöntem hello."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 6f931d94-ef5a-44c6-b1d9-8a3c9c327fb2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 1f5a4e724e00ea6d16f5511b9120154f89441758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-guide"></a>Azure depolama Güvenlik Kılavuzu
## <a name="overview"></a>Genel Bakış
Azure depolama toobuild güvenli uygulamalar birlikte, geliştiricilerin güvenlik özellikleri kapsamlı bir kümesini sağlar. Merhaba depolama hesabının kendisi rol tabanlı erişim denetimi ve Azure Active Directory kullanılarak güvenli hale getirilebilir. Veri güvenli bir uygulama ile Azure arasında aktarımda kullanarak [istemci tarafı şifreleme](../storage-client-side-encryption.md), HTTPS veya SMB 3.0. Veriler yazılırken otomatik olarak şifrelenir toobe ayarlanabilir depolama tooAzure kullanarak [depolama hizmeti şifreleme (SSE)](storage-service-encryption.md). Sanal makineler tarafından kullanılan işletim sistemi ve veri diskleri kullanılarak şifrelenmiş toobe ayarlanabilir [Azure Disk şifrelemesi](../../security/azure-security-disk-encryption.md). Atanmış erişim toohello veri nesneleri Azure Depolama olanağı verilir kullanarak [paylaşılan erişim imzaları](../storage-dotnet-shared-access-signature-part-1.md).

Bu makalede Azure Storage ile kullanılabilmesi için bu güvenlik özelliklerin her biri bir bakış sağlar. Bağlantılar kolayca yapabilirsiniz, böylece her bir özelliğin ayrıntılarını verecektir tooarticles sağlanan araştırma her konu hakkında daha fazla.

Bu makalede ele alınan hello konuları toobe şunlardır:

* [Yönetim düzlemi güvenlik](#management-plane-security) – depolama hesabınızın güvenliğini sağlama

  Merhaba Yönetim düzeyi hello kullanılan kaynakları toomanage depolama hesabınız oluşur. Bu bölümde, biz hello Azure Resource Manager dağıtım modeli ve nasıl toouse rol tabanlı erişim denetimi (RBAC) toocontrol erişim tooyour depolama hesapları hakkında konuşun. Biz, depolama hesabı anahtarlarını yönetme hakkında konuşur ve nasıl tooregenerate bunları.
* [Veri düzlemi güvenliği](#data-plane-security) – erişimi güvenli hale getirme tooYour veri

  Bu bölümde, biz erişim toohello gerçek veri nesneleri depolama hesabınızdaki BLOB'lar, dosyalar, kuyruklar ve tablolar gibi izin vermeyi paylaşılan erişim imzaları ve depolanan erişim ilkeleri kullanarak göreceğiz. Hizmet düzeyi SAS ve hesap düzeyinde SAS ele alınacaktır. Ayrıca nasıl toolimit erişim tooa belirli bir IP adresi (veya IP adresi aralığı) tooHTTPS toolimit hello protokolü kullanılan nasıl ve ne göreceğiz için bekleyen olmadan bir paylaşılan erişim imzası toorevoke tooexpire.
* [Aktarım Sırasında Şifreleme](#encryption-in-transit)

  Bu bölümde ele alınmaktadır nasıl içine veya dışına Azure Storage aktardığınızda toosecure veri. Azure dosya paylaşımları için SMB 3.0 tarafından kullanılan şifreleme HTTPS ve hello kullanımını önerilen hello hakkında konuşun. Biz de dışında depolama aktarıldıktan sonra bir istemci uygulamasında depolama alanına aktarılır önce tooencrypt hello verileri ve toodecrypt hello verileri sağlayan istemci tarafı şifreleme göz atın.
* [Bekleme Sırasında Şifreleme](#encryption-at-rest)

  Biz depolama hizmeti şifreleme (SSE) ve nasıl, blok blobları, sayfa bloblarını kaynaklanan bir depolama hesabı için etkinleştirmek ve ne zaman tooAzure depolama yazılmış ekleme blobları otomatik olarak Şifrelenmekte hakkında konuşur. Ayrıca Azure Disk şifrelemesi kullanın ve hello temel farklar ve istemci tarafı şifreleme karşı SSE karşı Disk şifrelemesi örneklerini keşfedin nasıl ele alacağız. Kısaca ABD için FIPS uyumluluk ele alacağız Kamu bilgisayarlar.
* Kullanarak [depolama çözümlemeleri](#storage-analytics) tooaudit erişim Azure depolama

  Bu bölümde hello depolama çözümlemeleri toofind bilgileri için bir istek nasıl günlüğe yazacağını anlatılmaktadır. Biz günlük verilerinin gerçek depolama çözümlemeleri göz atın ve nasıl toodiscern bir istekte olup olmadığını hello depolama Bkz hesap anahtarla bir paylaşılan erişim imzası veya anonim olarak ve olup başarılı veya başarısız oldu.
* [Tarayıcı tabanlı istemcileri CORS kullanarak etkinleştirme](#Cross-Origin-Resource-Sharing-CORS)

  Bu bölümde ettiği hakkında tooallow çıkış noktaları arası kaynak paylaşımını (CORS). Etki alanları arası erişim ve nasıl toohandle hello CORS yetenekleri ile Azure depolama alanına yerleşik hakkında konuşun.

## <a name="management-plane-security"></a>Yönetim düzlemi güvenliği
Merhaba Yönetim düzeyi hello depolama hesabı kendisini etkileyen işlemden oluşur. Örneğin, oluşturmak veya bir depolama hesabı silebilir, depolama hesaplarının bir listesiyle bir abonelik almak, hello depolama hesabı anahtarlarını almak veya hello depolama hesabı anahtarlarını yeniden.

Yeni bir depolama hesabı oluşturduğunuzda, Klasik veya Resource Manager dağıtım modelini seçin. Azure kaynakları oluşturma hello Klasik modeli yalnızca ya hep ya hiç erişim toohello abonelik sağlar ve buna karşılık, depolama hesabı hello.

Bu kılavuz anlamına gelir, depolama hesapları oluşturmak için önerilen hello olan hello Resource Manager modeli odaklanır. Merhaba Resource Manager depolama hesapları, erişim toohello tüm abonelik vermiş yerine, rol tabanlı erişim denetimi (RBAC) kullanarak daha sınırlı bir düzey toohello Yönetim düzeyi erişimi denetleyebilirsiniz.

### <a name="how-toosecure-your-storage-account-with-role-based-access-control-rbac"></a>Nasıl toosecure depolama hesabı rol tabanlı erişim denetimi ile (RBAC)
Şimdi RBAC nedir ve nasıl kullanabileceğiniz hakkında konuşun. Her Azure aboneliği bir Azure Active Directory’ye sahiptir. Kullanıcılar, gruplar ve uygulamalar bu dizinden erişim toomanage hello Resource Manager dağıtım modeli kullanmanız hello Azure aboneliği kaynaklarında verilebilir. Başvurulan tooas rol tabanlı erişim denetimi (RBAC) budur. toomanage bu erişimi, hello kullanabilirsiniz [Azure portal](https://portal.azure.com/), hello [Azure CLI araçlarını](../../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), veya hello [Azure depolama kaynak sağlayıcısı REST API'leri ](https://msdn.microsoft.com/library/azure/mt163683.aspx).

Merhaba Resource Manager modeli ile bir kaynak grubu ve Denetim erişim toohello Yönetim düzeyi Azure Active Directory'yi kullanarak, belirli bir depolama hesabının içinde hello depolama hesabı yerleştirin. Örneğin, diğer kullanıcıların hello depolama hesabı bilgilerini görüntüleyebilirsiniz, ancak hello depolama hesabı anahtarlarını erişemiyor hello özelliği tooaccess hello depolama hesabı anahtarları, belirli kullanıcılara verebilirsiniz.

#### <a name="granting-access"></a>Erişim izni verme
Merhaba uygun RBAC rolü toousers, gruplar ve uygulamalar, hello doğru kapsamda atanarak erişim verilir. toogrant erişim toohello tüm abonelik, hello abonelik düzeyinde bir rol atayın. Bir kaynak grubunda hello kaynakların erişim tooall izinleri toohello kaynak grubu kendisini vererek verebilirsiniz. Ayrıca, depolama hesapları gibi toospecific kaynakları belirli roller atayabilirsiniz.

RBAC tooaccess hello yönetim işlemlerini Azure Storage hesabı kullanma hakkında tooknow gereken hello ana noktalar şunlardır:

* Erişim atadığınızda, temelde toohave erişim istediğiniz bir rol toohello hesabına atayın. Bu depolama hesabı erişim toohello kullanılan işlemleri toomanage kontrol edebilirsiniz, ancak hello hesabında değil toohello veri nesneleri. Örneğin, tooretrieve hello özelliklerini hello depolama hesabını (örneğin, artıklık), ancak değil tooa kapsayıcı veya Blob Storage içindeki bir kapsayıcı içindeki veri izni verebilirsiniz.
* Birinin toohave izin tooaccess hello hello depolama hesabındaki veri nesneleri, izni tooread hello depolama hesabı anahtarlarını verin ve bu kullanıcı daha sonra bu anahtarları tooaccess hello BLOB, kuyruklar, tablolar ve dosyaları kullanabilirsiniz.
* Rolleri atanabilir tooa belirli bir kullanıcı hesabı, bir grup kullanıcılar veya tooa belirli bir uygulama.
* Her rol Eylemler ve değil eylemlerinin bir listesi vardır. Örneğin, "listKeys" eylemini hello sanal makine katkıda bulunan rolü sahiptir, böylece hello depolama hesabı anahtarları toobe okuyun. Merhaba erişim hello Active Directory kullanıcılar için güncelleştirilmesi gibi "Değil Eylemler" Merhaba katkıda bulunan var.
* Depolama için rolleri dahil (ancak bunlarla sınırlı değildir) hello aşağıdaki:

  * Sahibi – bunlar erişim dahil her şeyi yönetebilir.
  * Katkıda bulunan – yapabilecekleri şeylerin herhangi bir şey hello sahibi, Ata erişim dışındaki. Bu role sahip biri görüntüleyebilir ve hello depolama hesabı anahtarlarını yeniden. Merhaba depolama hesabı anahtarları ile bunların hello veri nesneleri erişebilir.
  * Okuyucu – gizli dışında hello depolama hesabıyla ilgili bilgileri görüntüleyebilirler. Örneğin, hello depolama hesabı toosomeone okuyucu izinlerine sahip bir rol atarsanız, hello hello depolama hesabının özelliklerini görüntüleyebilirsiniz, ancak herhangi bir değişiklik toohello özellikleri veya hello depolama hesabı anahtarlarını görüntüleyin.
  * Depolama hesabı katkıda bulunan – bunlar hello depolama hesabı yönetebilir – bilgi edinebilirsiniz hello aboneliğin kaynak grupları ve kaynakları oluşturmak ve abonelik kaynak grubu dağıtımlarını yönetin. Bunlar, sırayla hello veri düzlemi erişebilecekleri anlamına gelir hello depolama hesabı anahtarlarını da erişebilirsiniz.
  * Kullanıcı erişimi Yöneticisi – bunlar kullanıcı erişimi toohello depolama hesabını yönetebilir. Örneğin, okuyucu tooa belirli kullanıcıya erişim izni verebilir.
  * Sanal makine Katılımcısı – bunlar sanal makineler ancak bunlar bağlı değil hello depolama hesabı toowhich yönetebilirsiniz. Bu rol hello depolama hesabı anahtarları, bu rol atama kullanıcı toowhom hello anlamına hello veri düzlemi güncelleştirebilirsiniz listeleyebilirsiniz.

    Bir kullanıcı toocreate bir sanal makine için sırayla toobe mümkün toocreate hello karşılık gelen VHD dosyasında bir depolama hesabı sahiptirler. toobe mümkün tooretrieve hello depolama gerekir, toodo anahtarı hesap ve hello VM oluşturma toohello API geçirin. Bu nedenle, hello depolama hesabı anahtarlarını listeleyebilirsiniz şekilde bu izni olmalıdır.
* Merhaba özelliği toodefine özel roller toocompose Azure kaynakları gerçekleştirilebilir kullanılabilir eylemler listesinden Eylemler kümesi sağlayan bir özelliktir.
* Merhaba kullanıcı rolü toothem atamadan önce Azure Active Directory'yi ayarlama toobe sahiptir.
* Kimin verilen/grafikten kim ve PowerShell kullanarak hangi kapsamında erişim türüne iptal bir rapor oluşturduğunuzda veya Azure CLI hello.

#### <a name="resources"></a>Kaynaklar
* [Azure Active Directory Rol Tabanlı Erişim Denetimi](../../active-directory/role-based-access-control-configure.md)

  Bu makalede hello açıklanmaktadır Azure Active Directory rol tabanlı erişim denetimi ve nasıl çalışır.
* [RBAC: Yerleşik Roller](../../active-directory/role-based-access-built-in-roles.md)

  Bu makalede hello yerleşik roller RBAC'de kullanılabilen tüm ayrıntılarını verir.
* [Resource Manager dağıtımını ve klasik dağıtımı anlama](../../azure-resource-manager/resource-manager-deployment-model.md)

  Bu makalede hello Resource Manager dağıtımını ve klasik dağıtım modellerine açıklar ve hello Resource Manager ve kaynak grupları kullanmanın yararları hello açıklanmaktadır. Bu, hello Azure işlem, ağ ve depolama sağlayıcıları hello Resource Manager modeli altında nasıl çalıştığı açıklanmıştır.
* [Rol tabanlı erişim denetimini hello REST API ile yönetme](../../active-directory/role-based-access-control-manage-access-rest.md)

  Bu makalede nasıl toouse hello REST API toomanage RBAC gösterilmektedir.
* [Azure depolama kaynak sağlayıcısı REST API Başvurusu](https://msdn.microsoft.com/library/azure/mt163683.aspx)

  Merhaba toomanage program aracılığıyla depolama hesabınızı kullanabilirsiniz API'leri hello başvurusunu budur.
* [Geliştirici Kılavuzu tooauth Azure Kaynak Yöneticisi API'si](http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/)

  Bu makalede nasıl tooauthenticate kullanarak izin ver hello Resource Manager API'leri gösterir.
* [Ignite’tan Microsoft Azure için Rol Tabanlı Erişim Denetimi](https://channel9.msdn.com/events/Ignite/2015/BRK2707)

  Bağlantı tooa hello 2015 MS Ignite Konferanstan Channel 9 video budur. Bu oturumda, bunlar hakkında konuşun erişim yönetimi ve Azure raporlama özellikleri ve tooAzure abonelikleri Azure Active Directory'yi kullanarak erişimi güvenli hale getirme geçici en iyi yöntemler keşfedin.

### <a name="managing-your-storage-account-keys"></a>Depolama hesabı anahtarlarını yönetme
Depolama hesabı anahtarları, birlikte hello depolama hesap adı, Azure tarafından oluşturulan 512 bit dizelerdir hello depolama hesabı, örn. BLOB, tablo, kuyruk iletileri ve bir Azure dosya paylaşımında varlıkları depolanan kullanılan tooaccess hello veri nesneleri olabilir. Denetleme erişim toohello depolama hesabı anahtarları denetimleri toohello veri düzlemi bu depolama hesabı için erişim.

Her Depolama hesabı başvurulan iki anahtar tooas "Anahtar 1" ve "2 anahtar" hello sahip [Azure portal](http://portal.azure.com/) ve hello PowerShell cmdlet'leri. Bunlar, bunlarla sınırlı toousing hello dahil olmak üzere birkaç yöntemden birini kullanarak el ile yeniden üretilebilir [Azure portal](https://portal.azure.com/), .NET depolama istemci kitaplığı hello veya Azure hello PowerShell, hello Azure CLI veya programlı olarak kullanma Storage Hizmetleri REST API'si.

Depolama hesabı anahtarları nedeniyle tooregenerate herhangi bir sayıda vardır.

* Bunları düzenli güvenlik nedenleriyle yeniden.
* Birisi bir uygulamaya toohack yönetilen ve tam erişim tooyour depolama hesabı vermiş sabit kodlanmış veya bir yapılandırma dosyasında kaydedilen hello anahtarı almak, depolama hesabı anahtarlarını yeniden.
* Ekibinizin hello depolama hesabı anahtarı koruyan bir Depolama Gezgini uygulama kullanıyor ve hello ekip üyelerinin birini bırakır anahtarını yeniden üretme işlemi için başka bir durumdur. Merhaba uygulaması kaldırılmıştır sonra erişim tooyour depolama hesabı onların toowork devam eder. Bu hesap düzeyinde paylaşılan erişim imzaları oluşturulan gerçekte hello birincil nedeni – yapılandırma dosyasında hello erişim anahtarlarını depolamak yerine bir hesap düzeyinde SAS kullanabilirsiniz.

#### <a name="key-regeneration-plan"></a>Anahtarını yeniden üretme planı
Bazı planlama olmadan kullanıyorsanız toojust üretme hello anahtar istemezsiniz. Bunu yaparsanız önemli kesintiye neden tüm erişim toothat depolama hesabı devre dışı, kesin. İki anahtar vardır nedeni budur. Aynı anda bir anahtar anahtarını yeniden oluşturmalısınız.

Anahtarlarınızı yeniden önce tüm hello depolama hesabında bağımlı olan uygulamalar, aynı zamanda Azure'da kullandığınız diğer hizmetler listesine sahip emin olun. Depolama hesabınıza bağlı olan bir Azure Media Services kullanıyorsanız, hello anahtarı yeniden oluşturduktan sonra gibi hello erişim tuşlarını medya hizmetlerinizle yeniden eşitlemeniz gerekir. Bir Depolama Gezgini gibi herhangi bir uygulama kullanıyorsanız, tooprovide hello yeni anahtarları toothose uygulamalar da gerekir. VHD dosyaları hello depolama hesabında depolanır Vm'leriniz varsa, bunlar hello depolama hesabı anahtarlarını yeniden oluşturma tarafından etkilenmez olduğunu unutmayın.

Anahtarlarınızı hello Azure portal'ın yeniden oluşturabilirsiniz. Anahtarları yeniden sonra too10 sürebilir dakika toobe depolama hizmetleri arasında eşitlenir.

Hazır olduğunuzda, anahtarınızı nasıl değiştiğini ayrıntılı hello Genel süreç şöyledir. Bu durumda, hello anahtar 1 kullanmakta olduğunuz ve her şeyi toochange adımıdır varsayılır toouse 2 yerine anahtar.

1. Güvenli anahtar 2 tooensure yeniden oluşturun. Hello Azure portal bunu yapabilirsiniz.
2. Tüm hello depolama anahtarı depolandığı hello uygulamaları hello depolama anahtar toouse anahtar 2'in yeni değeri değiştirin. Sınama ve yayımlama hello uygulama.
3. Tüm Merhaba, uygulamaları ve Hizmetleri hazır olduğunuzda ve başarıyla çalışıyor anahtar 1 yeniden. Bu, herkes, açıkça verilmemiş hello yeni anahtarı toowhom artık olacaktır sağlar erişim toohello depolama hesabı.

Anahtar 2 kullanıyorsanız, aynı ters hello anahtar adları işlemi hello kullanabilirsiniz.

Her uygulama toouse hello yeni anahtarı değiştirme ve yayımlamadan gün, birkaç geçirebilirsiniz. Hepsini tamamladıktan sonra daha sonra geri dönün ve böylece artık çalışır hello eski anahtarı yeniden gerekir.

Başka bir seçenektir tooput hello depolama hesabı anahtarı bir [Azure anahtar kasası](https://azure.microsoft.com/services/key-vault/) gizli olarak ve buradan, uygulamaların alınamıyor hello anahtara sahip. Merhaba anahtarını yeniden oluşturmak ve hello Azure anahtar kasası güncelleştirme hello uygulamaları bunlar hello yeni anahtarı hello Azure anahtar Kasası'ndan otomatik olarak seçer çünkü imzalanmasını toobe gerekmez. Hello anahtar ihtiyacınız okuyamayacağı hello uygulama sahip olabilir veya bellekte önbelleğe ve, kullanırken başarısız olursa hello anahtarı yeniden hello Azure anahtar Kasası ' alıp unutmayın.

Azure anahtar kasası kullanarak başka bir depolama anahtarları için güvenlik düzeyi ekler. Bu yöntemi kullanırsanız, birisi toohello anahtarları belirli izinsiz erişim sağlama, o avenue kaldıran bir yapılandırma dosyası, hiçbir zaman hello depolama anahtar sabit kodlanmış gerekir.

Azure anahtar kasası kullanarak başka bir avantajı, Azure Active Directory'yi kullanarak erişim tooyour anahtarlarını kontrol edebilirsiniz olmasıdır. Başka bir deyişle, tooretrieve hello anahtarları Azure anahtar kasası gerekir ve diğer uygulamalar özellikle izin verme olmadan mümkün tooaccess hello anahtarları olmaz bildikleri uygulamaları toohello sayıda erişim izni verebilir.

Not: hello birini tüm uygulamalarınızın Merhaba, aynı anahtarları yalnızca toouse önerilir zaman. Bazı yerlerde anahtar 1 ve diğer anahtar 2 kullanıyorsanız, yapmamayı anahtarlarınızı erişimi kaybetmenize bazı uygulama olmadan mümkün toorotate olabilir.

#### <a name="resources"></a>Kaynaklar
* [Azure Storage hesapları hakkında](storage-create-storage-account.md#regenerate-storage-access-keys)

  Bu makalede, depolama hesapları genel bir bakış sağlar ve görüntüleme, kopyalama ve depolama erişim anahtarlarını yeniden anlatılmaktadır.
* [Azure depolama kaynak sağlayıcısı REST API Başvurusu](https://msdn.microsoft.com/library/mt163683.aspx)

  Bu makale hello REST API kullanarak bir Azure hesabı için bağlantılar toospecific makaleleri alınırken hello depolama hesabı anahtarlarını yeniden oluşturuluyor hello depolama hesabı anahtarları hakkında içerir. Not: Resource Manager depolama hesapları için budur.
* [Depolama hesapları işlemleri](https://msdn.microsoft.com/library/ee460790.aspx)

  Bu makalede hello depolama Service Manager REST API Başvurusu alma ve hello REST API kullanarak hello depolama hesabı anahtarlarını yeniden oluşturma bağlantılar toospecific makaleleri içerir. Not: Hello Klasik depolama hesapları için budur.
* [Güle güle tookey yönetim söyleyin – Azure AD kullanarak erişim tooAzure depolama verileri yönetme](http://www.dushyantgill.com/blog/2015/04/26/say-goodbye-to-key-management-manage-access-to-azure-storage-data-using-azure-ad/)

  Bu makalede toouse Active Directory toocontrol erişim nasıl tooyour Azure Storage anahtarları Azure anahtar Kasası'gösterir. Aynı zamanda, nasıl toouse bir Azure Otomasyonu işi tooregenerate hello anahtarları saatlik düzenli olarak gösterir.

## <a name="data-plane-security"></a>Veri düzlemi güvenliği
Veri düzlemi güvenliği Azure Storage – hello BLOB, kuyruklar, tablolar ve dosyaları kullanılan toosecure hello veri nesneleri depolanan toohello yöntemleri gösterir. Yöntemleri tooencrypt hello veri ve güvenlik hello veri aktarım sırasında gördük ancak toohello nesneleri erişimine hakkında olduğunu nasıl gittiğiniz?

Temel olarak kontrol eden erişim toohello veri nesnelerinin kendileri için iki yöntem vardır. Merhaba ilk denetleme erişim toohello depolama hesabı anahtarları tarafından olduğu ve Merhaba, ikinci paylaşılan erişim imzaları toogrant erişim toospecific veri nesneleri belirli bir süre kullanıyor.

Bir özel durum toonote hello BLOB'ları uygun şekilde tutan hello kapsayıcı hello erişim düzeyini ayarlayarak genel erişim tooyour BLOB'lar izin verebilir ' dir. Kapsayıcı tooBlob ya da kapsayıcı erişimi ayarladıysanız, bu kapsayıcıdaki hello BLOB'lar için herkese okuma erişimi sağlar. Bu kapsayıcıdaki tooa blob'u işaret eden bir URL kimseyle bir tarayıcıda paylaşılan erişim imzası kullanarak veya hello depolama hesabı anahtarlarını sahip açmadan anlamına gelir.

### <a name="storage-account-keys"></a>Depolama Hesabı Anahtarları
Depolama hesabı anahtarlarını hello depolama hesabı adı ile birlikte kullanılan tooaccess hello veri nesneleri hello depolama hesabında depolanan olabilir, Azure tarafından oluşturulan 512 bit dizelerdir.

Örneğin, BLOB'lar okuyun, tooqueues yazma, tablolar oluşturmak ve dosyalarda değişiklik. Bu eylemler çoğunu hello Azure gerçekleştirilebilir portalı veya çok sayıda Depolama Gezgini uygulamalardan birini kullanarak. Bu işlemler kod toouse hello REST API veya hello depolama istemcisi kitaplıklarını tooperform biri de yazabilirsiniz.

Merhaba üzerinde Hello bölümünde açıklandığı gibi [yönetim düzlemi güvenlik](#management-plane-security), Klasik depolama hesabı tam erişim toohello Azure aboneliği vererek verilebilir için erişim toohello depolama anahtarları. Rol tabanlı erişim denetimi (RBAC) hello Azure Resource Manager modelini kullanarak bir depolama hesabı için erişim toohello depolama anahtarları denetlenebilir.

### <a name="how-toodelegate-access-tooobjects-in-your-account-using-shared-access-signatures-and-stored-access-policies"></a>Nasıl toodelegate erişim paylaşılan erişim imzaları ve depolanan erişim ilkeleri kullanarak hesabınızda tooobjects
Paylaşılan erişim imzası olabilir bir güvenlik belirteci içeren bir dize tooa toodelegate erişim toostorage nesnelerine izin veren URI bağlı olan ve kısıtlamaları gibi hello izinler ve erişim hello tarih aralığını belirtin.

Erişim tooblobs, kapsayıcıları, iletileri kuyruğa, dosyaları ve tabloları erişim izni verebilir. Tablolarla, aslında izni tooaccess varlıklar hello tablosundaki bir dizi hello kullanıcı toohave erişimi istediğiniz hello bölüm ve satır anahtar aralıklarına toowhich belirterek verebilirsiniz. Coğrafi durumu ile bir bölüm anahtarı depolanan verileri varsa, örneğin, birisi toojust hello verilere erişmek için California sağlayabilir.

Başka bir örnekte, bir web uygulaması toowrite girişleri tooa sıra sağlayan bir SAS belirteci vermek ve bir alt hello SAS belirteci tooget iletilerden sıraya almak ve bunları işlemek rol uygulama verin. Ya da bunlar tooupload resimleri tooa kapsayıcısı içinde Blob Storage kullanma ve bir web uygulaması izin tooread bu resimlerinizi verin bir SAS belirteci bir müşteri sunabilir. Her iki durumda da sorunları ayrılması yoktur – her bir uygulama içinde gereksinim duydukları yalnızca hello erişim verilebilir tooperform görevini sipariş. Bu paylaşılan erişim imzaları hello kullanımla mümkün olur.

#### <a name="why-you-want-toouse-shared-access-signatures"></a>Toouse paylaşılan erişim imzaları neden istediğiniz
Neden toouse yalnızca çok daha kolaydır, depolama hesabı anahtarınızı vermiş yerine bir SAS istiyor? Depolama hesabı anahtarınızı vermiş, depolama Krallık hello anahtarları gibi paylaşımıdır. Tam erişim verir. Birisi anahtarlarınızı kullanın ve tüm Müzik Kitaplığı tooyour depolama hesaplarında yükleyin. Bunlar de virüs bulaşmış sürümleri ile dosyalarınızı değiştirmek veya verilerinizi çalabilir. Sınırsız erişimi tooyour depolama hesabı hemen vermiş, hafifçe alınmamalıdır şeydir.

Paylaşılan erişim imzaları ile bir istemci yalnızca sınırlı bir süre için gereken hello izinleri verebilirsiniz. Örneğin, birisi blob tooyour hesabı karşıya varsa, bunları (Merhaba blob hello boyutunu Elbette bağlı olarak) yeterli zaman tooupload hello blob yazma erişimi verebilirsiniz. Ve fikrinizi değiştirirseniz, o erişimi iptal edebilirsiniz.

Ayrıca, SAS kullanılarak yapılan istekleri IP adresi veya IP adres aralığı dış tooAzure belirli kısıtlı tooa olduğunu belirtebilirsiniz. Ayrıca, belirli bir Protokolü (HTTPS veya HTTP/HTTPS) kullanarak isteklerinin yapılma isteyebilirsiniz. Bu, yalnızca tooallow HTTPS trafiği istediğiniz yalnızca gerekli hello Protokolü tooHTTPS ayarlayabilirsiniz ve HTTP trafiği engellenecek anlamına gelir.

#### <a name="definition-of-a-shared-access-signature"></a>Paylaşılan erişim imzası tanımı
Paylaşılan erişim imzası hello kaynağa işaret eden toohello URL'si sorgu parametreleri kümesini eklenmiş olan

izin verilen ve hangi Merhaba erişimine izin verilen süreyi hello hello erişim hakkında bilgi sağlar. Örnek aşağıda verilmiştir; Bu URI beş dakika okuma erişimi tooa blob sağlar. SAS parametreleri sorgu Not URL kodlanmış, iki nokta üst üste (:) veya bir alan için % %20 3A gibi olması gerekir.

```
http://mystorage.blob.core.windows.net/mycontainer/myblob.txt (URL toohello blob)
?sv=2015-04-05 (storage service version)
&st=2015-12-10T22%3A18%3A26Z (start time, in UTC time and URL encoded)
&se=2015-12-10T22%3A23%3A26Z (end time, in UTC time and URL encoded)
&sr=b (resource is a blob)
&sp=r (read access)
&sip=168.1.5.60-168.1.5.70 (requests can only come from this range of IP addresses)
&spr=https (only allow HTTPS requests)
&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D (signature used for hello authentication of hello SAS)
```

#### <a name="how-hello-shared-access-signature-is-authenticated-by-hello-azure-storage-service"></a>Nasıl paylaşılan erişim imzası kimlik doğrulaması tarafından hello hello Azure depolama hizmeti
Merhaba depolama hizmeti hello isteği aldığında, hello giriş sorgu parametrelerini alır ve bir imza oluşturur kullanarak hello aynı yöntemini çağıran program hello gibi. Ardından, hello iki imzaları karşılaştırır. Kabul ediyorum sonra hello depolama hizmeti hello depolama hizmeti sürüm toomake geçerli olduğundan emin denetleyin, hello geçerli tarih ve saat içinde hello belirtilen pencere, istenen yapma emin hello erişim karşılık gelen yapılan toohello istek, vb. olduğunu doğrulayın.

Merhaba URL bir blob yerine tooa dosyasında işaret ediyorsanız için blob paylaşılan erişim imzası olan, hello belirttiğinden Örneğin, yukarıdaki bizim URL ile bu isteği başarısız olur. Merhaba çağrılan REST komutunu tooupdate bir blob ise, hello paylaşılan erişim imzası yalnızca okuma erişimi verilip belirttiğinden başarısız olur.

#### <a name="types-of-shared-access-signatures"></a>Paylaşılan erişim imzaları türleri
* Bir hizmet düzeyi SAS kullanılan tooaccess belirli bir depolama hesabı kaynaklarında olabilir. Bu, bazı örnekler BLOB'ları bir kapsayıcıda listesi alınıyor, bir blob yükleme, bir tablodaki bir varlık güncelleştiriliyor, iletileri tooa sırası ekleme veya dosya tooa dosya paylaşımı karşıya yükleme.
* Bir hesap düzeyinde SAS kullanılan tooaccess bir hizmet düzeyi SAS kullanılabilir herhangi bir şey olabilir. Ayrıca, hello özelliği toocreate kapsayıcılar, tablolar, kuyruklar ve dosya paylaşımları gibi bir hizmet düzeyi SAS ile izin verilmiyor seçenekleri tooresources verebilirsiniz. Erişim toomultiple Hizmetleri aynı anda de belirtebilirsiniz. Örneğin, birisi erişim tooboth BLOB'ları ve dosya depolama hesabınızdaki size.

#### <a name="creating-an-sas-uri"></a>Bir SAS URI'sini oluşturma
1. Tüm hello Sorgu parametrelerinin her tanımlama, isteğe bağlı bir geçici URI oluşturabilirsiniz.

   Bu gerçekten esnek, ancak bir mantıksal parametrelerinin her zaman benzer varsa, depolanan bir Erişim İlkesi'ni kullanarak daha iyi bir fikir.
2. Bir kapsayıcının tamamı, dosya paylaşımı, tablo veya kuyruğu için depolanan bir erişim ilkesi oluşturabilirsiniz. Ardından, bu hello temel olarak SAS oluşturduğunuz URI'ler hello için kullanabilirsiniz. Depolanan erişim ilkelerine bağlı olarak izinleri kolayca iptal edilebilir. Sağlayabilirsiniz yukarı her kapsayıcısı, kuyruk, tablo veya dosya paylaşımı üzerinde tanımlanan too5 ilkeleri.

   Örneğin, toohave olmaz birçok kişi hello BLOB'lar belirli bir kapsayıcıda okuma, bir depolanan erişim "okuma erişimi verin" diyen ilkesi oluşturabilir ve her zaman aynı olacak herhangi bir ayarı hello. Daha sonra bir SAS hello depolanmış erişim ilkesi hello ayarları kullanarak ve hello süre sonu tarihi/saati belirterek URI oluşturabilirsiniz. Merhaba bu avantajlarından toospecify yok olduğundan her zaman tüm hello sorgu parametreleri.

#### <a name="revocation"></a>İptal etme
SAS açığa çıktıysa veya toochange istediğinizi varsayalım, Kurumsal güvenlik veya yasal uyumluluk gereksinimleri nedeniyle. Bu SAS kullanarak erişim tooa kaynak nasıl iptal edilsin mi? Bu, hello SAS URI'sini nasıl oluşturulacağını bağlıdır.

Geçici URI'si kullanıyorsanız, üç seçeneğiniz vardır. Kısa süre sonu ilkeleriyle SAS belirteçleri ve yalnızca hello SAS tooexpire için bekleyin. Yeniden adlandırma veya hello kaynak (Merhaba belirteci kapsamlı tooa tek nesne olduğu varsayılarak) silin. Merhaba depolama hesabı anahtarlarını değiştirebilirsiniz. Bu son seçeneği kaç Hizmetleri bu depolama hesabı kullanıyorsanız bağlı olarak büyük bir etkisi olabilir ve büyük olasılıkla bazı planlama olmadan toodo istediğiniz bir şey değil.

Depolanan bir erişim ilkesi tarafından türetilmiş bir SAS kullanıyorsanız, hello depolanmış erişim ilkesi iptal ederek erişimi kaldırabilirsiniz – yalnızca süresi dolmuş veya tamamen kaldırmak için değiştirebilirsiniz. Bu hemen etkili olur ve bu depolanmış erişim ilkesi kullanılarak oluşturulan her SAS geçersiz kılar. Güncelleştirme veya kaldırma hello depolanan erişim ilkesi, belirli bir kapsayıcıya, dosya paylaşımı, tablo veya kuyruğu SAS aracılığıyla erişen kişilerin etkileyebilir, ancak hello hello eskisinin geçersiz hale geldiğinde yeni bir SAS istediklerinde böylece istemciler yazılır, bu düzgün çalışır.

Depolanan bir erişim ilkesi tarafından türetilmiş SAS kullanarak verdiğinden SAS hemen, bu en iyi yöntem tooalways hello önerilen olduğunu hello özelliği toorevoke depolanan erişim ilkeleri mümkün olduğunda kullanın.

#### <a name="resources"></a>Kaynaklar
Paylaşılan erişim imzaları ve depolanan erişim ilkeleri, örnekler, tam kullanma hakkında daha ayrıntılı bilgi için lütfen aşağıdaki makaleleri toohello başvurun:

* Merhaba Başvurusu makalelerine bunlar.

  * [Hizmet SAS](https://msdn.microsoft.com/library/dn140256.aspx)

    Bu makale bir hizmet düzeyi SAS BLOB'lar, iletileri kuyruğa, tablo aralıkları ve dosyaları kullanma örnekleri sağlar.
  * [Hizmet SAS oluşturma](https://msdn.microsoft.com/library/dn140255.aspx)
  * [Hesap SAS oluşturma](https://msdn.microsoft.com/library/mt584140.aspx)
* Merhaba .NET istemci kitaplığı toocreate paylaşılan erişim imzaları ve depolanan erişim ilkeleri kullanma öğreticileri bunlar.

  * [Paylaşılan erişim imzaları (SAS) kullanma](../storage-dotnet-shared-access-signature-part-1.md)
  * [Paylaşılan erişim imzası, bölüm 2: Oluşturma ve bir SAS hello Blob hizmeti ile kullanma](../blobs/storage-dotnet-shared-access-signature-part-2.md)

    Bu makale, bir açıklama hello SAS modelini, paylaşılan erişim imzaları örnekleri içermektedir ve hello en iyi uygulama önerileri SAS kullanın. Ayrıca ele alınan hello izni hello iptal olur.
* IP adresi (IP ACL'ler) tarafından erişimi sınırlandırma

  * [Bir uç nokta erişim denetimi listesi (ACL) nedir?](../../virtual-network/virtual-networks-acl.md)
  * [Hizmet SAS oluşturma](https://msdn.microsoft.com/library/azure/dn140255.aspx)

    Hizmet düzeyi SA'ları için hello başvurusu makalesinde budur; IP başarısız örneği içerir.
  * [Hesap SAS oluşturma](https://msdn.microsoft.com/library/azure/mt584140.aspx)

    Hesap düzeyinde SA'ları için hello başvurusu makalesinde budur; IP başarısız örneği içerir.
* Kimlik Doğrulaması

  * [Hello Azure Storage Hizmetleri için kimlik doğrulaması](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* Paylaşılan erişim imzası öğretici Başlarken

  * [SAS öğretici Başlarken](https://github.com/Azure-Samples/storage-dotnet-sas-getting-started)

## <a name="encryption-in-transit"></a>Aktarımdaki şifreleme
### <a name="transport-level-encryption--using-https"></a>Aktarım düzeyinde şifreleme – HTTPS kullanarak
Azure Storage verilerinizin tooensure hello güvenliğini almanız gereken başka bir adım tooencrypt hello Azure Storage ile Merhaba istemci arasında verilerdir. Merhaba ilk önerilir tooalways kullanmak hello [HTTPS](https://en.wikipedia.org/wiki/HTTPS) hello genel Internet protokolü üzerinden güvenli iletişim sağlar.

Merhaba REST API'leri çağırma veya erişme depolama nesneleri toohave güvenli bir iletişim kanalı, her zaman HTTPS kullanmanız gerekir. Ayrıca, **paylaşılan erişim imzaları**, kullanılan toodelegate olabilen tooAzure depolama nesnelere erişmek, HTTPS protokolünü kullanılabilir herkes sağlanarak paylaşılan erişim imzaları kullanırken, yalnızca hello seçeneği toospecify içerir SAS belirteci bağlantılarıyla dışarı gönderme hello uygun protokolünü kullanır.

Merhaba REST API'leri tooaccess nesneleri depolama hesaplarında etkinleştirerek çağrılırken HTTPS hello kullanılmasını zorunlu kılabilir [güvenli aktarımı gerekli](../storage-require-secure-transfer.md) hello depolama hesabı için. Bu özellik etkinleştirildiğinde, HTTP kullanarak bağlantı reddedilecek.

### <a name="using-encryption-during-transit-with-azure-file-shares"></a>Azure dosya paylaşımları ile aktarım sırasında şifreleme kullanma
Azure File storage HTTPS hello REST API kullanırken destekler, ancak bir SMB dosya paylaşımına tooa VM bağlı olarak daha yaygın olarak kullanılır. SMB 2.1 bağlantıları yalnızca hello içinde aynı izin için şifrelemeyi desteklemiyor Azure bölgesinde. Ancak, SMB 3.0 Şifreleme destekler ve Windows Server 2012 R2'de kullanılabilir, Windows 8, Windows 8.1 ve Windows 10, çapraz bölge izin vererek erişmek ve erişim hello masaüstünde bile.

Azure dosya paylaşımları ile UNIX kullanılabilse de, erişimi yalnızca bir Azure bölgesi içinde izin hello Linux SMB istemci henüz şifreleme desteklemediğini unutmayın. Linux için şifreleme desteği hello yol haritası Linux geliştiriciler için SMB işlevselliği sorumlu açıktır. Şifreleme eklediğinizde, olacaktır hello Windows için yaptığınız gibi Linux üzerinde bir Azure dosya paylaşımına erişmek için aynı özelliği.

Etkinleştirerek şifreleme hello Azure dosya hizmeti ile Merhaba kullanılmasını zorunlu kılabilir [güvenli aktarımı gerekli](../storage-require-secure-transfer.md) hello depolama hesabı için. Merhaba REST API'lerini kullanarak, HTTPs gereklidir. SMB için şifrelemeyi destekleyen SMB bağlantıları başarıyla bağlanır.

#### <a name="resources"></a>Kaynaklar
* [Nasıl toouse Linux Azure File storage](../storage-how-to-use-files-linux.md)

  Bu makalede nasıl toomount bir Azure dosya paylaşımı bir Linux sistem ve karşıya yükleme/yükleme dosyalarını gösterilmektedir.
* [Windows'da Azure Dosya Depolama ile çalışmaya başlama](../storage-dotnet-how-to-use-files.md)

  Bu makalede Azure dosya paylaşımları genel bir bakış sağlar ve nasıl toomount ve bunları PowerShell ve .NET kullanarak.
* [Azure Dosya depolama incelemesi](https://azure.microsoft.com/blog/inside-azure-file-storage/)

  Bu makalede, Azure dosya depolama alanının hello genel kullanılabilirlik sunar ve hello SMB 3.0 şifreleme hakkında teknik ayrıntılar sağlar.

### <a name="using-client-side-encryption-toosecure-data-that-you-send-toostorage"></a>İstemci tarafı şifreleme toosecure veri toostorage Gönder kullanma
Bir istemci uygulaması ve depolama arasında aktarılırken verilerinizin güvenli olduğundan emin olun yardımcı olan başka bir istemci tarafı şifreleme seçenektir. Merhaba veriler Azure depolama alanına aktarılmadan önce şifrelenir. Hello istemci tarafında alındıktan sonra hello verileri Azure depolama biriminden alırken, hello verilerin şifresi çözülür. İçinde Yardım hello hello verilerin bütünlüğünü etkileyen ağ hataları azaltmak yerleşik veri bütünlük denetimlerinin olduğu gibi hello kablo giderek Hello veri şifrelenir olsa bile, ayrıca, HTTPS kullanmanızı öneririz.

Merhaba veriler şifrelenmiş biçimde depolanır istemci tarafı şifreleme Ayrıca, rest, verileri şifrelemek için bir yöntem aynıdır. Biz bu konuda hello bölümünde daha ayrıntılı üzerinde konuşun [bekleyen şifreleme](#encryption-at-rest).

## <a name="encryption-at-rest"></a>Bekleyen şifreleme
Bekleyen şifreleme sağlayan üç Azure özellikleri vardır. Azure Disk şifrelemesi kullanılan tooencrypt hello işletim sistemi ve veri diskleri olarak Iaas sanal makineleri ' dir. diğer iki hello – istemci tarafı şifreleme ve SSE – hem kullanılan tooencrypt verileri Azure Storage'dır. Şimdi her birinde, arayın ve ardından bir karşılaştırma yapmak ve her birinin ne zaman kullanılabilir bakın.

(Hangi ayrıca depolama, şifrelenmiş biçimde depolanır) aktarım istemci tarafı şifreleme tooencrypt hello veri kullanabilmenize karşın, hello aktarım sırasında HTTPS toosimply kullanım tercih ve bazı yolu olduğunda otomatik olarak şifrelenir hello veri toobe için yoktur depolanır. Vardır iki yolu toodo bu--Azure Disk şifrelemesi ve SSE. Bir kullanılan toodirectly VM'ler tarafından kullanılan işletim sistemi ve veri disklerde hello verileri şifrelemek ve hello diğer olduğu tooAzure Blob Storage yazılan kullanılan tooencrypt veriler.

### <a name="storage-service-encryption-sse"></a>Depolama hizmeti şifrelemesi (SSE)
SSE toorequest hello depolama hizmeti otomatik olarak hello veri tooAzure depolama yazılırken şifrelemenizi sağlar. Merhaba verileri Azure depolama alanından okuyun, onu hello depolama hizmeti tarafından döndürülen önce şifresi çözülür. Bu, verilerinizi toomodify kalmadan kod veya kod tooany uygulamalar eklemek toosecure sağlar.

Toohello tüm depolama hesabı geçerli bir ayar budur. Etkinleştirin ve hello ayarı hello değerini değiştirerek bu özelliği devre dışı. toodo bunu hello Azure portalı, PowerShell hello Azure CLI kullanıyorsanız, depolama kaynak sağlayıcısı REST API hello veya .NET depolama istemci kitaplığı hello. Varsayılan olarak, SSE kapalıdır.

Şu anda hello anahtarları hello şifreleme için kullanılan Microsoft tarafından yönetilir. Biz başlangıçta hello anahtarlar oluşturmak ve iç Microsoft İlkesi tarafından tanımlanan, hello normal döndürme yanı sıra hello anahtarları hello güvenli depolama yönetin. Hello gelecekteki, kendi şifreleme anahtarlarınızı hello özelliği toomanage alın ve toocustomer yönetilen anahtarları anahtarlardan Microsoft tarafından yönetilen bir geçiş yolu sağlar.

Bu özellik hello Resource Manager dağıtım modeli kullanılarak oluşturulan standart ve Premium depolama hesapları için kullanılabilir. SSE ekleme blobları ve sayfa BLOB'ları yalnızca tooblock BLOB'lar geçerlidir. Merhaba diğer tablolar, kuyruklar ve dosyaları da dahil olmak üzere veri türleri şifrelenmez.

Veriler yalnızca SSE etkin olduğunda ve tooBlob depolama hello veriler yazılır şifrelenir. Etkinleştirme veya devre dışı bırakma SSE mevcut verileri etkilemez. Diğer bir deyişle, bu şifreleme etkinleştirdiğinizde, bu değil geri dönün ve zaten verileri şifrelemek; veya SSE devre dışı bıraktığınızda, zaten hello verilerin şifresini.

Bu özellik Klasik depolama hesabına sahip toouse istiyorsanız, yeni bir Resource Manager depolama hesabı oluşturun ve AzCopy toocopy hello veri toohello yeni hesabı kullanın.

### <a name="client-side-encryption"></a>İstemci tarafı şifreleme
İstemci tarafı şifreleme Aktarımdaki hello verileri hello şifrelenmesi ele alırken belirtiliyor. Bu özellik, tooprogrammatically tooAzure depolama yazılmış hello kablo toobe göndermeden önce bir istemci uygulaması verilerinizi şifrelemek ve tooprogrammatically Azure depolama biriminden aldıktan sonra verilerinizi şifresini sağlar.

Bu şifreleme Aktarımdaki sağlar, ancak REST şifreleme hello özelliği de sağlar. Merhaba veriler aktarım sırasında şifrelenir, ancak hala HTTPS tootake avantajı, ağ hataları hello hello verilerin bütünlüğünü etkileyen azaltmaya yardımcı olmak hello yerleşik veri bütünlüğü denetimlerini kullanarak öneririz olduğunu unutmayın.

Bu burada kullanabileceğinize bir örnek BLOB'lar depolar ve BLOB'ları alır bir web uygulamasına sahip ve hello uygulama ve veri toobe olabildiğince güvenli istediğiniz ' dir. Bu durumda, istemci tarafı şifreleme kullanırsınız. şifrelenmiş hello kaynak hello Azure Blob hizmeti ile Merhaba istemci arasında Hello trafiği içerir ve hiç kimse aktarım hello verileri yorumlama ve özel bloblarınızın yeniden oluşturma.

İstemci tarafı şifreleme hello Java ve sırayla hello oldukça, tooimplement kolaylaştırır Azure anahtar kasası API'lerini kullanan hello .NET depolama istemci kitaplıkları, yerleşik olarak bulunur. şifreleme ve hello verilerin şifresini çözmek hello işleminde hello Zarf tekniği kullanır ve her depolama nesnesindeki hello şifreleme tarafından kullanılan meta verileri depolar. Örneğin, BLOB'ları için bunu depoladığı hello blob meta verilerde sırada sıralar, bunu, tooeach kuyruk iletisi ekler.

Merhaba şifreleme için kendisini oluşturmak ve kendi şifreleme anahtarlarınızı yönetin. Azure Storage istemci kitaplığı hello tarafından üretilen anahtarlar de kullanabilirsiniz veya sağlayabilirsiniz hello Azure anahtar kasası hello anahtarları oluşturur. Şirket içi anahtar depolama şifreleme anahtarlarınızı depolayabilir veya bir Azure anahtar kasası depolayabilirsiniz. Azure anahtar kasası toogrant erişim toohello gizli anahtarları Azure anahtar kasası toospecific kullanıcıların Azure Active Directory'yi kullanarak sağlar. Bu, yalnızca herkes hello Azure anahtar kasası okuma ve böylelikle, istemci tarafı şifreleme için kullanmakta olduğunuz hello anahtarlarını alma anlamına gelir.

#### <a name="resources"></a>Kaynaklar
* [Şifrelemek ve şifresini çözmek Azure anahtar kasası kullanılarak Microsoft Azure Storage blobları](../blobs/storage-encrypt-decrypt-blobs-key-vault.md)

  Bu makalede gösterilmektedir nasıl toouse istemci tarafı şifreleme nasıl toocreate KEK hello ve PowerShell kullanarak hello kasasına depolamak dahil olmak üzere Azure anahtar kasası ile.
* [Microsoft Azure depolama için istemci tarafı şifreleme ve Azure anahtar kasası](../storage-client-side-encryption.md)

  Bu makalede, bir istemci tarafı şifreleme açıklamasını verir ve hello depolama istemci kitaplığı tooencrypt ve şifre çözme kaynaklardan hello dört depolama hizmetleri kullanma örnekleri sağlar. Ayrıca, Azure anahtar kasası hakkında alınmaktadır.

### <a name="using-azure-disk-encryption-tooencrypt-disks-used-by-your-virtual-machines"></a>Azure Disk Şifrelemesi'ni kullanarak tooencrypt diskleri kullanılan, sanal makineleriniz tarafından
Azure Disk şifrelemesi yeni bir özelliktir. Bu özellik tooencrypt hello işletim sistemi ve bir Iaas sanal makine tarafından kullanılan veri disklerle sağlar. Windows için hello sürücüler, endüstri standardı BitLocker şifreleme teknolojisi kullanılarak şifrelenir. Linux için hello diskleri hello DM-Crypt teknolojisi kullanılarak şifrelenir. Bu Azure anahtar kasası tooallow ile toocontrol tümleşik ve hello disk şifreleme anahtarlarını yönetme.

Microsoft Azure'da etkinleştirildiğinde senaryoları Iaas VM'ler için aşağıdaki hello Hello çözümünü destekler:

* Azure anahtar kasası ile tümleştirme
* Standart katmanı VMs: [A, D, DS, G, GS ve benzeri serisi Iaas VM'ler](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Windows ve Linux Iaas VM'ler üzerinde şifrelemeyi etkinleştirme
* Windows Iaas VM'ler için sürücüler işletim sistemi ve veri şifreleme devre dışı bırakma
* Veri sürücülerini şifreleme Linux Iaas VM'ler için devre dışı bırakma
* Windows istemci işletim sistemi çalıştıran bir Iaas Vm'leri üzerinde şifrelemeyi etkinleştirme
* Bağlama yolları birimlerle şifrelemeyi etkinleştirme
* Linux (RAID) mdadm kullanarak bölümlemesine diskle yapılandırılmış sanal makineleri üzerinde şifrelemeyi etkinleştirme
* Veri diskleri için LVM kullanarak Linux VM'ler üzerinde şifrelemeyi etkinleştirme
* Depolama alanları kullanılarak yapılandırılan Windows VM'ler üzerinde şifrelemeyi etkinleştirme
* Tüm Azure genel bölgeleri desteklenir

Merhaba çözüm senaryoları, özellikleri ve teknoloji hello sürümde aşağıdaki hello desteklemez:

* Temel katman Iaas VM'ler
* Bir işletim sistemi sürücüsünde Linux Iaas VM'ler için şifrelemeyi devre dışı bırakma
* Merhaba Klasik VM oluşturma yöntemini kullanarak oluşturduğunuz Iaas VM'ler
* Şirket içi anahtar yönetimi hizmeti ile tümleştirme
* Azure dosya depolama (paylaşılan dosya sistemi), ağ dosya sistemi (NFS), dinamik birimler ve yazılım tabanlı RAID sistemler ile yapılandırılmış Windows VM'ler


> [!NOTE]
> Linux işletim sistemi disk şifrelemesi Linux dağıtımları aşağıdaki hello üzerinde şu anda desteklenmiyor: RHEL 7.2, CentOS 7.2n ve Ubuntu 16.04.
>
>

Bu özellik, sanal makine disklerdeki tüm veriler şifrelenir, Azure Storage REST sağlar.

#### <a name="resources"></a>Kaynaklar
* [Windows ve Linux Iaas VM'ler için Azure Disk şifrelemesi](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="comparison-of-azure-disk-encryption-sse-and-client-side-encryption"></a>Azure Disk şifrelemesi, SSE ve istemci tarafı şifreleme karşılaştırması
#### <a name="iaas-vms-and-their-vhd-files"></a>Iaas Vm'leri ve bunların VHD dosyaları
Iaas VM'ler tarafından kullanılan diskler için Azure Disk şifrelemesi kullanmanızı öneririz. Bu disklerin Azure storage'da kullanılan tooback olan SSE tooencrypt hello üzerinde VHD dosyalarını açabilirsiniz, ancak yalnızca yeni yazılmış verileri şifreler. Bu bir VM oluşturun ve ardından SSE hello VHD dosyasını tutan hello depolama hesabında etkinleştirirseniz, yalnızca hello değişiklikler şifrelenmiş anlamına gelir, özgün VHD dosyasını hello değil.

Hello Azure Marketi görüntüden kullanarak bir VM'i oluşturursanız, Azure gerçekleştiren bir [kopyalama yüzeysel](https://en.wikipedia.org/wiki/Object_copying) SSE etkin olsa bile hello görüntü tooyour Azure Storage ve bu depolama hesabında şifrelenmez. Merhaba VM oluşturur ve hello görüntüsünü güncelleştirme başlatır, SSE hello veri şifreleme başlar. Bu nedenle, bunları tam olarak şifrelenmiş istiyorsanız Azure Disk şifrelemesi vm'lerde hello Azure Market görüntülerini oluşturulan en iyi toouse değil.

Şirket içinden Azure'a önceden şifrelenmiş VM getirirseniz, mümkün tooupload hello şifreleme anahtarları tooAzure anahtar kasası olabilir ve şirket içi kullanmakta olduğunuz o VM için hello şifreleme kullanmaya devam. Azure Disk şifrelemesi etkin toohandle bu senaryodur.

Şirket içi şifrelenmemiş VHD'den varsa, özel bir görüntü olarak hello Galerisi içine yüklemek ve bir VM'den sağlayın. Merhaba Resource Manager şablonları kullanarak bunu yaparsanız, VM hello yüklediğinde, onu tooturn Azure Disk şifrelemesi sorabilirsiniz.

Bir veri diski ekleyin ve hello VM üzerinde bağlama, bu veri diskte Azure Disk şifrelemesi kapatabilirsiniz. Bu veri diski yerel olarak ilk şifreler ve hello depolama içerik şifrelenmiş şekilde hello Hizmet Yönetim katmanı geç yazma depolama karşı sonra ne yapacağını.

#### <a name="client-side-encryption"></a>İstemci Tarafında Şifreleme
İstemci tarafı şifreleme Aktarımdaki önce şifreler ve rest hello verileri şifreler, veri şifreleme hello en güvenli yöntemdir. Değil isteyebilirsiniz depolama kullanan kodu tooyour uygulamalar ekleme ancak gerektirir toodo. Bu durumlarda, Aktarımdaki verileri ve rest SSE tooencrypt hello verileri HTTPs kullanabilirsiniz.

İstemci tarafı şifreleme ile tablo varlıkları, iletileri kuyruğa ve blobları şifreleyebilirsiniz. SSE ile BLOB'ları yalnızca şifreleyebilirsiniz. Şifrelenmiş tablo ve kuyruk veri toobe gerekiyorsa, istemci tarafı şifreleme kullanmanız gerekir.

İstemci tarafı şifreleme tamamen hello uygulama tarafından yönetilir. Bu hello en güvenli yaklaşım, ancak toomake programsal değişiklikler tooyour uygulama gerektirir ve anahtar yönetimi işlemleri yerleştirdiniz. Merhaba istediğinizde bu kullanırsınız ve geçiş sırasında ek güvenlik şifrelenmiş, depolanan verilerin toobe istiyor.

İstemci tarafı şifreleme hello istemcide daha fazla yük, ve özellikle, şifreleme ve çok miktarda veri aktarma, tooaccount bu ölçeklenebilirlik planlarınızı sahip.

#### <a name="storage-service-encryption-sse"></a>Depolama hizmeti şifrelemesi (SSE)
SSE Azure Storage tarafından yönetilir. Merhaba güvenlik hello veri aktarım SSE kullanarak sağlamaz, ancak tooAzure depolama yazıldığı şekilde hello verileri şifreliyor. Üzerinde etkisi yoktur hello performans üzerinde bu özelliği kullanırken.

Yalnızca blok blobları şifreleme, ekleme blobları ve SSE kullanarak blob'lara sayfa. Tooencrypt tablo veya kuyruğu verilerini gerekiyorsa, istemci tarafı şifreleme kullanmayı düşünün.

Bir arşiv veya kitaplık yeni sanal makineler oluşturmak için temel olarak kullanmak VHD dosyalarının varsa, yeni bir depolama hesabı oluşturmak, SSE etkinleştirmek ve hello VHD dosyaları toothat hesabı karşıya yükleyin. Bu VHD dosyalarını Azure Storage tarafından şifrelenir.

Bir VM ve hello VHD dosyalarını tutan hello depolama hesabında etkin SSE hello diskler için Azure Disk şifrelemesini etkinleştirmişseniz düzgün çalışır; Bu iki kez Şifrelenmekte herhangi yeni yazılan veri kaybına neden.

## <a name="storage-analytics"></a>Depolama Analizi
### <a name="using-storage-analytics-toomonitor-authorization-type"></a>Storage Analytics toomonitor yetkilendirme türünü kullanma
Her Depolama hesabı için Azure Storage Analytics tooperform günlüğe yazılmasını etkinleştirmek ve ölçüm verilerini depolar. Bir depolama hesabı toocheck hello performans ölçümlerini istediğiniz veya performans sorunları yaşıyor çünkü tootroubleshoot bir depolama hesabı ihtiyacınız olduğunda harika aracı toouse budur.

Başka bir parça hello depolama analytics günlüklerinde görebilirsiniz veri depolama eriştiklerinde birisi tarafından kullanılan hello kimlik doğrulama yöntemidir. Örneğin, paylaşılan erişim imzası veya hello depolama hesabı anahtarlarını kullandıysanız ya da erişilen hello blob ortak ' da, bir Blob Storage'ı görebilirsiniz.

Bu erişim toostorage sıkı bir şekilde kullanılan koruyarak gerçekten yardımcı olabilir. Örneğin, Blob depolama alanına Merhaba kapsayıcılara tooprivate tümünün ayarlayın ve uygulamalarınızı hello hizmeti kullanımı için bir SAS uygulamak. Ardından hello düzenli olarak bloblarınızın bir güvenlik açığını gösterebilir, hello depolama hesabı anahtarları kullanılarak erişilir veya hello BLOB'lar ortak ancak bunlar olmamalıdır toosee günlüklerini denetleyin.

#### <a name="what-do-hello-logs-look-like"></a>Merhaba günlüklerini nasıl göründüğünü?
Sonra hello depolama hesabı ölçümlerini etkinleştirmeniz ve hello Azure portal günlüğü, analiz verileri tooaccumulate hızlı bir şekilde başlar. Merhaba günlüğe kaydetme ve ölçümleri her hizmet için ayrı; Merhaba günlük olduğunda etkinlik bu depolama hesabında hello ölçümleri dakikada, her saat veya nasıl yapılandırdığınıza bağlı olarak, her gün kaydedilir ancak yalnızca yazılır.

Merhaba günlükleri blok blobları hello depolama hesabındaki $logs adlı bir kapsayıcıda depolanır. Storage Analytics etkinleştirilmişse, bu kapsayıcı otomatik olarak oluşturulur. Bu kapsayıcı oluşturulduktan sonra içeriği silebilir ancak bunu silemezsiniz.

Merhaba $logs kapsayıcısı altında her hizmet için bir klasör yoktur ve ardından vardır alt hello yıl/ay/gün/saattir. Saat altında hello günlükleri yalnızca numaralandırılır. Hangi hello budur dizin yapısını gibi görünür:

![Günlük dosyalarını görüntüle](./media/storage-security-guide/image1.png)

Her istek tooAzure depolama günlüğe kaydedilir. Bir anlık görüntü hello ilk birkaç alanları gösteren bir günlük dosyası aşağıda verilmiştir.

![Anlık görüntü bir günlük dosyası](./media/storage-security-guide/image2.png)

Her türlü çağrıları tooa depolama hesabı hello günlükleri tootrack kullanabileceğiniz görebilirsiniz.

#### <a name="what-are-all-of-those-fields-for"></a>İçin bu alanların tümünü nelerdir?
Merhaba günlükleri ve ne için kullanıldıkları birçok alanları hello hello listesini sağlar aşağıdaki hello kaynaklar listelenen bir makale yoktur. Alanları sırada hello listesi aşağıdadır:

![Bir günlük dosyası alanların anlık görüntü](./media/storage-security-guide/image3.png)

GetBlob hello girişlerinde ilginizi çalışıyoruz ve kimlikleri doğrulanır nasıl, böylece biz işlem türü "Get-Blob" girişlerini toolook gerekir ve hello isteği-durumunu denetleyin (4<sup>th</sup> sütun) ve hello yetkilendirme-type (8<sup>th</sup> sütun).

Örneğin, içinde ilk birkaç satırı yukarıdaki hello listesindeki Merhaba, hello isteği-status "Başarılı" ve "Merhaba Yetkilendirme türü doğrulanır". Başka bir deyişle, hello isteği hello depolama hesabı anahtarı kullanılarak doğrulandı.

#### <a name="how-are-my-blobs-being-authenticated"></a>Nasıl my BLOB'lar kimlik doğrulaması gerçekleştirilen?
Biz ilgilendiğiniz üç durumda sunuyoruz.

1. Merhaba blob geneldir ve paylaşılan erişim imzası olmadan bir URL kullanılarak erişilir. Bu durumda, hello isteği-status "AnonymousSuccess" ve "anonim" Merhaba Yetkilendirme türü.

   1.0; 2015-11-17T02:01:29.0488963Z; GetBlob; **AnonymousSuccess**; 200; 124; 37; **Anonim**; mystorage...
2. Merhaba blob özeldir ve paylaşılan erişim imzası ile kullanıldı. Bu durumda, hello isteği-status "SASSuccess" ve "sa" Merhaba Yetkilendirme-türü olan.

   1.0; 2015-11-16T18:30:05.6556115Z; GetBlob; **SASSuccess**; 200; 416; 64; **SAS**; mystorage...
3. Merhaba blob özel ve hello depolama anahtar kullanılan tooaccess: Bu. Bu durumda, hello isteği-durumudur "**başarı**"ve hello Yetkilendirme-türü"**kimliği doğrulanmış**".

   1.0; 2015-11-16T18:32:24.3174537Z; GetBlob; **Başarı**; 206 59; 22; **Kimliği doğrulanmış**; mystorage...

Merhaba Microsoft Message Analyzer tooview kullanın ve bu günlüklerini analiz edin. Arama ve filtreleme yetenekleri içerir. Örneğin, toosearch için isteyebilirsiniz hello kullanım beklediğiniz, ise GetBlob toosee örneklerini yani birisi değil eriştiği depolama hesabınız açamayacağı emin toomake.

#### <a name="resources"></a>Kaynaklar
* [Depolama Analizi](../storage-analytics.md)

  Bu makalede depolama çözümlemeleri genel bir bakış olduğu ve nasıl tooenable bunları.
* [Storage Analytics günlük biçimi](https://msdn.microsoft.com/library/azure/hh343259.aspx)

  Merhaba hello istek için kullanılan kimlik doğrulama türünü gösteren kimlik doğrulama-türü de dahil olmak üzere, Ayrıntılar kullanılabilir alanlar hello ve bu makalede hello depolama Analytics günlük biçimi gösterilmektedir.
* [İzleyici bir depolama hesabında hello Azure portalı](../storage-monitor-storage-account.md)

  Bu makalede gösterilmektedir nasıl ölçümlerini izleme ve günlüğe kaydetme için bir depolama hesabı tooconfigure.
* [Azure Storage ölçümleri ve günlüğe kaydetme, AzCopy ve ileti Çözümleyicisi'ni kullanarak uçtan uca sorun giderme](../storage-e2e-troubleshooting.md)

  Bu makalede hello Storage Analytics kullanarak sorun giderme hakkında konuşur ve nasıl toouse hello Microsoft Message Analyzer gösterir.
* [Microsoft Message Analyzer işletim kılavuzu](https://technet.microsoft.com/library/jj649776.aspx)

  Bu makalede hello Microsoft Message Analyzer hello başvurusunu ve bağlantıları tooa Öğreticisi, hızlı başlangıç ve Özellik Özeti içerir.

## <a name="cross-origin-resource-sharing-cors"></a>Çıkış Noktaları Arası Kaynak Paylaşımı (CORS)
### <a name="cross-domain-access-of-resources"></a>Kaynak etki alanları arası erişimi
Bir etki alanında çalışan bir web tarayıcısı farklı bir etki alanından bir kaynak için bir HTTP istek yaptığında, bu çıkış noktaları arası HTTP isteği çağrılır. Örneğin, contoso.com sunulan HTML sayfası fabrikam.blob.core.windows.net üzerinde barındırılan bir JPEG dosyası için istekte bulunur. Güvenlik nedenleriyle, tarayıcılar JavaScript gibi komut dosyaları ve başlatılan cross-origin HTTP istekleri kısıtlayın. Bu, bazı JavaScript kodları contoso.com web sayfasında bu jpeg fabrikam.blob.core.windows.net üzerinde istediğinde hello tarayıcı hello isteği vermez anlamına gelir.

Bu yaptığı Azure Storage ile toodo sahip mi? İyi, JSON veya XML veri dosyaları gibi statik varlıklar depolanıyorsa Blob depolamada bir depolama hesabı kullanarak Fabrikam olarak adlandırılan, hello etki alanı hello varlıklar için fabrikam.blob.core.windows.net olacaktır ve Merhaba contoso.com web uygulaması mümkün tooaccess olmayacak bunları Merhaba etki alanları farklı olduğundan JavaScript kullanıyor. Bu ayrıca hello JavaScript istemci tarafından işlenen JSON veri toobe döndüren toocall hello – gibi Table Storage – Azure depolama hizmetleri birini çalıştığınız olduğunda true olur.

#### <a name="possible-solutions"></a>Olası çözümler
Tek yönlü tooresolve tooassign "storage.contoso.com" toofabrikam.blob.core.windows.net gibi özel bir etki alanı budur. Merhaba, yalnızca bu özel etki alanı tooone depolama hesabı atayabileceğiniz bir sorundur. Ne hello varlıklar birden çok depolama hesaplarında depolanır?

Başka bir şekilde tooresolve hello depolama çağrıları için proxy olarak toohave hello web uygulama act budur. Bu dosya tooBlob depolama yüklüyorsanız Merhaba web uygulaması ya da yerel olarak yazma ve tooBlob depolama kopyalayın veya tamamını belleğe okuma ve tooBlob depolama yazma anlamına gelir. Alternatif olarak, yerel olarak hello dosyaları karşıya yükler ve tooBlob depolama yazan bir adanmış web uygulaması (örneğin, bir Web API) yazabilirsiniz. Her iki durumda da belirleme hello ölçeklenebilirlik ihtiyacı olduğunda bu işlev için tooaccount sahip.

#### <a name="how-can-cors-help"></a>CORS nasıl yardımcı olabilir?
Azure depolama tooenable CORS – arası kaynak paylaşımı kaynak sağlar. Her Depolama hesabı için bu depolama hesabı hello kaynaklara erişebilir etki alanları belirtebilirsiniz. Örneğin, yukarıda özetlenen Örneğimizde, biz CORS hello fabrikam.blob.core.windows.net depolama hesabında etkinleştirin ve tooallow erişim toocontoso.com yapılandırın. Ardından hello web uygulama contoso.com doğrudan fabrikam.blob.core.windows.net hello kaynaklara erişebilir.

Bir şey toonote CORS erişim verir, ancak tüm olmayan ortak erişim için depolama kaynakları gerekli olan kimlik doğrulaması sağlamaz ' dir. Bu yalnızca erişebileceği anlamına gelir ortak veya paylaşılan erişim imzası, vermiş dahil BLOB'lar hello uygun izni. Tabloları, kuyrukları ve dosya genel erişiminiz yok ve bir SAS gerektirir.

Varsayılan olarak, CORS tüm hizmetleri devre dışıdır. CORS hello REST API veya hello depolama istemci kitaplığı toocall hello yöntemleri tooset hello hizmet ilkelerinden birini kullanarak etkinleştirebilirsiniz. Bunu yaptığınızda, XML biçiminde bir CORS kuralı içerir. Merhaba Blob hizmeti için hello hizmet özelliklerini ayarlama işlemi için bir depolama hesabı kullanılarak ayarlanmış olan bir CORS kuralı bir örneği burada verilmiştir. Azure Storage için hello depolama istemci kitaplığı veya hello REST API'lerini kullanarak bu işlemi gerçekleştirebilir.

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Her satır anlamı şudur:

* **AllowedOrigins** bu hangi eşleşmeyen etki alanları istemek ve hello Depolama hizmetinden veri alma bildirir. Bu, veri contoso.com ve fabrikam.com belirli bir depolama hesabı için Blob depolama alanından isteyebilir söyler. Bu tooa joker de ayarlayabilirsiniz (\*) tüm etki alanları tooaccess tooallow ister.
* **AllowedMethods** bu hello hello isteği yaparken kullanılan yöntem (HTTP isteği fiiller) listesidir. Bu örnekte, yalnızca GET ve PUT izin verilir. Bu tooa joker ayarlayabilirsiniz (\*) tooallow tüm yöntemleri toobe kullanılır.
* **AllowedHeaders** bu kaynak etki alanı hello üstbilgileri hello isteği yapılırken belirtebilirsiniz hello isteğidir. Bu örnekte, x-ms-meta-hedef ve x-ms-meta-abc, x-ms-meta veri ile başlangıç tüm meta veri üstbilgileri izin verilir. Merhaba joker karakter (\*) hello herhangi üstbilgi başlayarak önek verilir belirtilen gösterir.
* **ExposedHeaders** bu hangi yanıt üstbilgilerini hello tarayıcı toohello isteği veren tarafından açılmamalıdır bildirir. Bu örnekte, başlayarak başlığı "x-ms - meta-" gösterilir.
* **MaxAgeInSeconds** hello en uzun süreyi hello denetim öncesi seçenekleri isteği bir tarayıcı önbelleğe alır budur. (Merhaba denetim öncesi isteği hakkında daha fazla bilgi için hello ilk makale aşağıya bakın.)

#### <a name="resources"></a>Kaynaklar
CORS hakkında daha fazla bilgi ve nasıl tooenable, bu kaynakları gözden geçirin.

* [Hello Azure Storage Hizmetleri Azure.com üzerindeki çıkış noktaları arası kaynak paylaşımı (CORS) desteği](../storage-cors-support.md)

  Bu makalede CORS ve nasıl tooset hello hello farklı depolama hizmetleri için kurallar genel bakış sağlar.
* [Merhaba MSDN'deki Azure Storage Hizmetleri için çıkış noktaları arası kaynak paylaşımı (CORS) desteği](https://msdn.microsoft.com/library/azure/dn535601.aspx)

  Merhaba başvuru belgeleri hello Azure Storage Hizmetleri için CORS desteğini budur. Bu bağlantılar tooarticles tooeach depolama birimi hizmeti, uygulama vardır ve bir örneği gösterir ve her bir öğesinde hello CORS dosya açıklar.
* [Microsoft Azure Storage: CORS Tanıtımı](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/02/03/windows-azure-storage-introducing-cors.aspx)

  Bu CORS tanışın ve gösteren bir bağlantı toohello ilk blog makaledir nasıl toouse onu.

## <a name="frequently-asked-questions-about-azure-storage-security"></a>Azure Storage güvenliği hakkında sık sorulan sorular
1. **Nasıl hello HTTPS protokolünü kullanamıyorsanız ı içine veya dışına Azure Storage aktarma hello BLOB'ları hello bütünlüğünü doğrulayabilir?**

   HTTP yerine HTTPS ve blok blobları çalıştığınız toouse gereken herhangi bir nedenden dolayı MD5 denetimi kullanabilirsiniz, toohelp aktarılan hello BLOB'ları hello bütünlüğünü doğrulayın. Bu ağ/aktarım katmanı hataları korumadan, ancak mutlaka Ara saldırılarla yardımcı olur.

   Aktarım düzeyi güvenlik sağlayan HTTPS kullanırsanız, MD5 denetimi kullanarak yedekli ve gereksiz.

   Daha fazla bilgi için lütfen hello denetleyin [Azure Blob MD5 genel bakış](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/02/18/windows-azure-blob-md5-overview.aspx).
2. **Merhaba ABD için FIPS uyumluluğu hakkında Kamu?**

   Merhaba Amerika Birleşik Devletleri Federal Bilgi İşleme Standardı (FIPS) kullanım için ABD tarafından onaylanan şifreleme algoritmalarını tanımlar Gizli verilerin hello koruma için Federal hükümeti bilgisayar sistemleri. FIPS etkinleştirme bir Windows server ya da Masaüstü modunu hello işletim sistemi yalnızca FIPS doğrulamalı şifreleme algoritmaları kullanılması gerektiğini bildirir. Uygulamanın uyumlu algoritmaları kullanıyorsa, hello uygulamaların çalışmamasına neden olur. With.NET Framework sürüm 4.5.2 veya hello bilgisayar FIPS modundayken sonraki Merhaba uygulaması otomatik olarak hello şifreleme algoritmaları toouse FIPS uyumlu algoritmaları yapar.

   Microsoft bırakır, tooeach müşteri toodecide olup tooenable FIPS modunda. Konu toogovernment düzenlemeleri tooenable FIPS modunda varsayılan olmayan müşteriler ilgi çekici bir neden yoktur inanıyoruz.

   **Kaynakları**

* [Neden biz "FIPS modunda" artık öneren değil](http://blogs.technet.com/b/secguide/archive/2014/04/07/why-we-re-not-recommending-fips-mode-anymore.aspx)

  Bu Web günlüğü makalesini FIPS genel bir bakış sağlar ve bunlar varsayılan olarak FIPS modunda neden etkinleştirmezseniz açıklanmaktadır.
* [FIPS 140 doğrulaması](https://technet.microsoft.com/library/cc750357.aspx)

  Bu makalede nasıl Microsoft ürünleri ve şifreleme modüllerini hello FIPS standart hello ABD uymak hakkında bilgiler sağlanmaktadır. Federal Hükümet.
* ["Sistem şifrelemesi: kullanım FIPS uyumlu algoritmaları şifreleme, kodlama ve imzalama için" güvenlik ayarları etkilerini Windows XP ve Windows'un sonraki sürümleri](https://support.microsoft.com/kb/811833)

  Bu makalede, FIPS modunda daha eski Windows bilgisayarları hello kullanımı hakkındaki alınmaktadır.
