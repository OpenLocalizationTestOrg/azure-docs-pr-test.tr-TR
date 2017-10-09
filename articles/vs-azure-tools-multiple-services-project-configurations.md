---
title: "aaaConfiguring birden çok hizmet yapılandırması kullanarak Azure projenize | Microsoft Docs"
description: "Nasıl tooconfigure bir Azure bulut hizmeti projesi hello ServiceDefinition.csdef ve ServiceConfiguration.cscfg dosyaları değiştirerek öğrenin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a4fb79ed-384f-4183-9f74-5cac257206b9
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 14222266093eb876db0ac9ce8d3d17a04c65d1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-your-azure-project-using-multiple-service-configurations"></a>Birden çok hizmet yapılandırmalarını kullanarak projenizi Azure yapılandırma
Bir Azure bulut hizmeti projesi iki yapılandırma dosyalarını içerir: ServiceDefinition.csdef ve ServiceConfiguration.cscfg. Bu dosyalar Azure bulut hizmeti uygulamanızla birlikte paketlenir ve tooAzure dağıtılır.

* Merhaba **ServiceDefinition.csdef** dosyası hello hello gereksinimleri içerdiği hangi rolleri de dahil olmak üzere, bulut hizmeti uygulaması için Azure ortamı gerektirdiği hello meta verileri içerir. Bu dosya ayrıca tooall örnekleri uygulanan yapılandırma ayarlarını içerir. Bu yapılandırma ayarları hello Azure hizmet barındırma çalışma zamanı API'sini kullanarak çalışma zamanında okuyabilir. Hizmetinizi Azure üzerinde çalışırken bu dosyayı güncelleştirilemiyor.
* Merhaba **ServiceConfiguration.cscfg** dosya hello hizmet tanımı dosyasında tanımlanan hello yapılandırma ayarları için değerleri ayarlar ve her bir rol örnekleri toorun hello sayısını belirtir. Azure'da, bulut hizmetinizin çalışırken bu dosyanın güncelleştirilebilir.

Hello Azure Araçları için Microsoft Visual Studio bu dosyalar tooset yapılandırma ayarlarını kullanabilirsiniz özellik sayfaları sağlar. tooaccess hello özellik sayfaları, Çözüm Gezgini'nde, hello Azure bulut hizmeti projesi altında hello rol başvuruyu çift tıklatın veya hello rol başvuru sağ tıklayın ve seçin **özellikleri**hello aşağıdaki şekilde gösterildiği gibi.

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

Merhaba şemaları hello hizmet tanımı ve hizmet yapılandırma dosyaları için temel alınan hello hakkında daha fazla bilgi için bkz [şema başvurusu](https://msdn.microsoft.com/library/azure/dd179398.aspx). Hizmet yapılandırması hakkında daha fazla bilgi için bkz: [tooConfigure Cloud Services nasıl](cloud-services/cloud-services-how-to-configure.md).

## <a name="configuring-role-properties"></a>Rol özelliklerini yapılandırma
Aşağıdaki bölümlerde hello işaret bazı farklar olsa da hello özellik sayfaları web rolü ve çalışan rolü için benzerdir.

Merhaba gelen **önbelleğe alma** yapılandırabileceğiniz sayfa, Azure Hizmetleri önbelleği hello.

### <a name="configuration-page"></a>Yapılandırma sayfası
Merhaba üzerinde **yapılandırma** sayfasında, bu özellikleri ayarlayabilirsiniz:

**Örnekleri**

Set hello **örneği** sayısı özelliği toohello hello hizmet, bu rol için çalışmalı örnek sayısı.

Set hello **VM boyutu** özelliği çok**ek küçük**, **küçük**, **orta**, **büyük**, veya **Çok büyük**.  Daha fazla bilgi için bkz: [Cloud Services boyutları](cloud-services/cloud-services-sizes-specs.md).

**Başlatma eylemi** (Web rolü yalnızca)

Hata ayıklama başlattığınızda, Visual Studio hello HTTP uç noktaları veya hello HTTPS uç noktaları ya da hem bir web tarayıcısı belirmelidir bu özellik toospecify ayarlayın.

yalnızca zaten rolünüz için bir HTTPS uç noktası tanımladıysanız Hello HTTPS uç noktası seçeneği kullanılabilir. Merhaba üzerinde bir HTTPS uç noktası tanımlayabilirsiniz **uç noktaları** özellik sayfası.

Bir HTTPS uç nokta zaten eklediyseniz hello HTTPS uç noktası seçeneği varsayılan olarak etkindir ve Visual Studio hata ayıklama, ayrıca, HTTP uç noktası için tooa tarayıcı başlattığınızda bu uç nokta için bir tarayıcı başlatır. Bu, her iki başlangıç seçeneklerini etkinleştirildiğini varsayar.

**Tanılama**

Varsayılan olarak, tanılama hello Web rolü için etkinleştirilir. Hello Azure bulut hizmeti projesi ve depolama hesabı toouse hello yerel depolama öykünücüsü ayarlanır. Hazır toodeploy tooAzure olduğunda hello Oluşturucu düğmesini seçebilir (**...** ) tooupdate hello depolama hesabı toouse hello bulutta Azure depolama. İsteğe bağlı veya otomatik olarak zamanlanan aralıklarla hello tanılama veri toohello depolama hesabı aktarabilirsiniz. Azure Tanılama hakkında daha fazla bilgi için bkz: [Azure Cloud Services ve sanal makineleri etkinleştirme tanılamada](cloud-services/cloud-services-dotnet-diagnostics.md).

## <a name="settings-page"></a>Ayarları sayfası
Merhaba üzerinde **ayarları** sayfasında, hizmetiniz için yapılandırma ayarları ekleyebilirsiniz. Yapılandırma, ad-değer çiftleri ayarlardır. Merhaba rolünde çalışan kodu okuyabilir, yapılandırma ayarlarınızı hello tarafından sağlanan sınıflarını kullanarak çalışma zamanında hello değerlerini [Azure yönetilen kitaplık](http://go.microsoft.com/fwlink?LinkID=171026). Özellikle, hello [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx) yöntemi adlı yapılandırma ayarı çalışma zamanında hello değeri döndürür.

### <a name="configuring-a-connection-string-tooa-storage-account"></a>Bir bağlantı dizesi tooa depolama hesabı yapılandırma
Hello depolama öykünücüsü veya bir Azure depolama hesabı için bağlantı ve kimlik doğrulama bilgileri sağlayan bir yapılandırma ayarı bir bağlantı dizesidir. Kodunuzu Azure depolama hizmetleri veri – başka bir deyişle, blob, kuyruk veya tablo verisi – bir rolde çalışan kodundan erişim gerekir olduğunda, bu depolama hesabı için bir bağlantı dizesi toodefine gerekir.

Tooan Azure depolama hesabı işaret eden bir bağlantı dizesi, tanımlı bir biçimi kullanmanız gerekir. Hakkında bilgi için bkz toocreate bağlantı dizeleri, [Azure Storage bağlantı dizelerini yapılandırma](storage/common/storage-configure-connection-string.md).

Zaman hazır tootest hizmetinizi hello Azure storage hizmetlerine karşı olan veya olduğunuzda, bulut hizmeti tooAzure toodeploy hazır, tüm bağlantı dizeleri toopoint tooyour Azure depolama hesabı hello değerini değiştirebilirsiniz. Seçin (**...** ), select **depolama hesabının kimlik bilgilerini girin**. Hesap adı ve hesap anahtarını içeren hesap bilgilerini girin. Merhaba, **depolama hesabı bağlantı dizesi** iletişim kutusunda, ayrıca belirtebilirsiniz toouse hello varsayılan HTTPS uç noktalarının (Merhaba varsayılan seçenek), hello varsayılan HTTP uç noktaları ya da özel uç noktaları istediğiniz. Özel etki alanı adı, hizmetiniz için kaydolduysanız açıklandığı gibi toouse özel uç noktaları göstermeyebilir [bir Azure depolama hesabında blob verileri için bir özel etki alanı adı yapılandırma](storage/blobs/storage-custom-domain-name.md).

> [!IMPORTANT]
> Hizmetinizi dağıtmadan önce bağlantı dizeleri toopoint tooan Azure depolama hesabı değiştirmeniz gerekir. Başarısız olan toodo bu rolünüze değil toostart neden olabilir veya toocycle aracılığıyla hello başlatılırken, meşgul ve durduruluyor durumlarını.
> 
> 

## <a name="endpoints-page"></a>Uç noktaları sayfası
Çalışan rolü herhangi bir sayıda HTTP, HTTPS veya TCP uç noktaları olabilir. Uç noktaları kullanılabilir tooexternal istemcileridir, giriş uç noktaları veya hello Hizmeti'nde çalışan kullanılabilir tooother rolleri, iç uç noktalar olabilir.

* toomake bir HTTP uç noktası kullanılabilir tooexternal istemcileri ve Web tarayıcıları hello uç nokta türü tooinput değiştirmek ve bir ad ve bir ortak bağlantı noktası numarası belirtin.
* toomake bir HTTPS uç noktası kullanılabilir tooexternal istemcileri ve Web tarayıcıları değiştirme hello uç nokta türü çok**giriş**, bir ad, bir ortak bağlantı noktası numarası ve bir yönetim sertifikası adı belirtin.
  
    Bir yönetim sertifikası belirtebilmeniz için önce üzerinde hello hello sertifika tanımlamanız gerekir Not **sertifikaları** özellik sayfası.
* toomake hello bulut hizmeti, diğer rollerdeki iç erişmek için kullanılabilir bir uç nokta hello uç nokta türü toointernal değiştirin ve bir ad ve bu uç nokta için olası özel bağlantı noktalarını belirtin.

## <a name="local-storage-page"></a>Yerel depolama sayfası
Merhaba kullanabilirsiniz **yerel depolama** özellik sayfası tooreserve bir veya daha fazla yerel depolama kaynaklarını bir rol için. Yerel depolama kaynağı hello dosya sistemi hello Azure sanal makinesi, ayrılmış dizinindedir olduğu bir rol örneği çalışır.

## <a name="certificates-page"></a>Sertifikalar sayfası
Merhaba üzerinde **sertifikaları** sayfasında, sertifikalar rolünüze ile ilişkilendirebilirsiniz. olabilir kullanılan tooconfigure hello üzerindeki HTTPS uç noktalarınızı eklediğiniz hello sertifikaları **uç noktaları** özellik sayfası.

Merhaba **sertifikaları** özellik sayfası sertifikaları tooyour hizmet yapılandırmanızla ilgili bilgi ekler. Hizmetiniz ile sertifikalarınızı paketlenmiş değil unutmayın; sertifikalarınızı ayrı olarak yüklemeniz gerekir hello aracılığıyla tooAzure [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).

tooassociate sizin rolünüz sertifikasıyla hello sertifika için bir ad sağlayın. Merhaba üzerinde bir HTTPS uç noktasını yapılandırdığınızda bu adı toorefer toohello sertifika kullanmak **uç noktaları** özellik sayfası. Ardından, hello sertifika deposu olup olmadığını belirtin **yerel makine** veya **geçerli kullanıcı** ve hello deposunun hello adı. Son olarak, hello sertifikanın parmak izini girin. Merhaba sertifika (My) deposunda hello geçerli User\Personal ise, hello sertifika doldurulan bir listeden seçerek hello sertifikanın parmak izi girebilirsiniz. Başka bir konumda bulunuyorsa, hello parmak izi değeri el ile girin.

Merhaba sertifika deposundan bir sertifikayı eklediğinizde, tüm ara sertifikaların toohello yapılandırma ayarları sizin için otomatik olarak eklenir. Ayrıca bu Ara sertifikaları karşıya yüklenen sipariş toocorrectly tooAzure hizmetiniz SSL için yapılandırın.

Yalnızca hello bulutta çalışırken hizmetiniz ile ilişkilendirmek istediğiniz yönetim sertifikaları tooyour hizmet uygulayın. Hizmetinizi hello yerel geliştirme ortamında çalışan hello işlem öykünücüsü tarafından yönetilen standart bir sertifika kullanır.

## <a name="configuring-hello-azure-cloud-service-project"></a>Hello Azure bulut hizmeti projesi yapılandırma
tooan tüm Azure bulut hizmeti projesi geçerli tooconfigure ayarları, önce bu proje düğümüne hello kısayol menüsünü açın ve sonra Özellikler tooopen özellik sayfalarının seçin. Aşağıdaki tablonun hello bu özellik sayfaları gösterir.

| Özellik sayfası | Açıklama |
| --- | --- |
| Uygulama |Bu sayfadan, bu bulut hizmeti projesini kullanan Azure Araçları hello sürümü hakkında bilgi görüntüleyebilir ve hello Araçları'nın geçerli sürümü toohello yükseltebilirsiniz. |
| Derleme olayları |Bu sayfadan oluşturma öncesi ve sonrası derleme olaylarını ayarlayabilirsiniz. |
| Geliştirme |Bu sayfadan yapı yapılandırma yönergeleri ve altında oluşturma sonrası olay çalıştırdığınız hello koşulları belirtebilirsiniz. |
| Web |Bu sayfadan toohello web sunucusu ile ilgili ayarları yapılandırabilirsiniz. |

