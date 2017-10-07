---
title: Visual Studio'da sunucusuz bir uygulama aaaBuild | Microsoft Docs
description: "İlk sunucusuz uygulamanızı oluşturma, dağıtma ve Visual Studio hello uygulamasını yönetme bu kılavuzu ile başlayın."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a>Visual Studio'da Logic Apps ve işlevleri ile sunucusuz bir uygulama oluşturun

Sunucusuz araçları ve Azure işlevleri hızlı geliştirme ve bulut uygulamalarının dağıtımını için izin verir.  Bu belge odaklanılmaktadır tooget Visual Studio sunucusuz bir uygulama oluşturmaya başladı.  Azure içinde sunucusuz bir genel bakış [bu makalede bulunabilir](logic-apps-serverless-overview.md).

## <a name="getting-everything-ready"></a>Her şeyi hazırlığı

Visual Studio'dan sunucusuz bir uygulama hello gerekli Önkoşullar toobuild şunlardır:

* [Visual Studio 2017](https://www.visualstudio.com/vs/) veya Visual Studio 2015 - Community, Professional veya Enterprise
* [Visual Studio için Logic Apps araçları](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* [En son Azure SDK'sı](https://azure.microsoft.com/downloads/) (2.9.1 veya üzeri)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* [Azure işlevleri çekirdek Araçları](https://www.npmjs.com/package/azure-functions-core-tools) toodebug işlevleri yerel olarak
* Mantıksal Uygulama Tasarımcısı Hello kullanırken erişim toohello web katıştırılmış

## <a name="getting-started-with-a-deployment-template"></a>Bir dağıtım şablonu ile çalışmaya başlama

Azure kaynakları yöneten bir kaynak grubu içindeki yapılır.  Bir kaynak grubu kaynakları mantıksal bir gruplandırmasıdır.  Kaynak grupları, dağıtım ve kaynak yönetimi sağlar.  Azure içinde sunucusuz bir uygulama için hem Azure mantıksal uygulamaları hem de Azure işlevleri bizim kaynak grubunu içerir.  Visual Studio içinde hello kaynak grubu projesi kullanarak mümkün toodevelop gerçekleştiriyoruz, yönetmek ve tek bir varlık olarak hello tüm uygulama dağıtmak.

### <a name="create-a-resource-group-project-in-visual-studio"></a>Visual Studio'da bir kaynak grubu projesi oluşturma

1. Visual Studio'da tooadd tıklatın bir **yeni proje**
1. Merhaba, **bulut** kategorisi, select toocreate Azure **kaynak grubu** proje  
 * Merhaba kategori veya listelenen proje görmüyorsanız hello Azure SDK'sı için Visual Studio yüklenmiş sahip olduğundan emin olun
1. Bir ad ve konum Hello proje verin ve seçin **Tamam** toocreate Visual Studio tooselect şablon ister.  Boş, başlangıç mantığı uygulama ile veya başka kaynaklara toostart seçebilirsiniz.  Ancak, bu durumda bize sunucusuz bir uygulama ile başlatılan bir Azure Hızlı Başlangıç şablonu tooget kullanırız.
1. Tooshow şablonları arasından seçim **Azure Hızlı Başlangıç** ![seçerek Azure hızlı başlangıç şablonları][1]
1. Select hello sunucusuz hızlı başlatma şablonunu: **101-logic-app-and-function-app** tıklatıp **Tamam**

Merhaba Hızlı Başlangıç şablonu kaynak grubu projenizi bir dağıtım şablonu oluşturur.  Azure işlevleri çağırır ve hello sonuç döndüren basit bir mantıksal uygulama Hello şablonu içerir.  Merhaba açarsanız `azuredeploy.json` dosyasında Merhaba Çözüm Gezgini, hello sunucusuz uygulaması için hello kaynaklarını görebilirsiniz.

## <a name="deploying-hello-serverless-application"></a>Merhaba sunucusuz bir uygulama dağıtma

Visual Studio'da hello mantıksal uygulama görsel tasarımcı açmadan önce toobe önceden dağıtılan Azure kaynak grubu gerekir.  Bu, hello mantıksal uygulama hello Tasarımcı toocreate ve kullanım bağlantıları tooresources ve hizmetleri sağlar.  başlatılan tooget, biz oluşturulan toodeploy hello çözüm yeterlidir.

1. Visual Studio'da seçin sağ hello projesi **dağıtma**ve oluşturma bir **yeni** dağıtım ![yeni kaynak dağıtım seçme][2]
1. Geçerli bir Azure abonelik ve kaynak grubu seçin
1. Çok seçin**dağıtma** hello çözümü
1. Merhaba mantıksal uygulama Hello adını ve hello Azure işlev uygulaması girin.  Hello Azure işlev adı toobe genel benzersiz mu

Merhaba sunucusuz çözüm hello belirtilen kaynak grubuna dağıtır.  Merhaba bakarsanız **çıkış** Visual Studio'da hello dağıtım hello durumunu görebilirsiniz.

## <a name="editing-hello-logic-app-in-visual-studio"></a>Visual Studio'da Hello mantıksal uygulama düzenleme

Merhaba çözüm herhangi bir kaynak grubu dağıtıldıktan sonra hello görsel tasarımcı kullanılan tooedit olması ve değişiklikleri toohello mantıksal uygulama hale getirebilirsiniz.

1. Sağ hello `azuredeploy.json` dosya hello Çözüm Gezgini ve seçin **ile Logic Apps tasarımcıyı Aç**
1. Select hello **kaynak grubu** ve **konumu** hello çözüm süredir tooand seçin dağıtılan **Tamam**

Merhaba mantıksal uygulama görsel tasarımcı artık Visual Studio ile görünür olması gerekir.  Tooadd adımlara devam etmeden, hello iş akışı değiştirin ve değişiklikleri kaydedin.  Visual Studio'dan mantıksal uygulamalar da oluşturabilirsiniz.  Merhaba sağ tıklattığınızda, **kaynakları** hello şablon Gezgini'nde tooadd seçebileceğiniz bir **mantıksal uygulama** toohello proje.  Boş mantıksal uygulamalar yük hello visual Tasarımcısı'nda bir kaynak grubuna ön dağıtımını yap.

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a>Yönetme ve çalıştırma geçmişi dağıtılan mantıksal uygulama için görüntüleme

Ayrıca, yönetmek ve logic apps Azure'de dağıtılan hello çalıştırma geçmişini görüntülemek.  Merhaba açarsanız **Cloud Explorer** aracı Visual Studio'da, tüm mantıksal uygulama sağ tıklayın ve tooedit, devre dışı bırakma, Görünüm Özellikleri seçin ya da görünümü çalıştırma geçmişi.  Düzen'i tıklatarak bir Visual Studio kaynak grubu projesine toodownload yayımlanan mantıksal uygulama, sağlar.  Bu mantıksal uygulamanızı hello Azure portal oluşturmaya başladı olsa bile, yine, içeri aktarabilir ve Visual Studio'dan yönetmek, anlamına gelir.

## <a name="developing-an-azure-function-in-visual-studio"></a>Visual Studio'da bir Azure işlevinizi geliştirme

Merhaba dağıtım şablonu dağıtır hello belirtilen hello git deposu için hello çözümde bulunan tüm Azure işlevleri `azuredeploy.json` değişkenleri.  Merhaba çözümünde işlevi proje yazarsanız, kaynak denetimine (GitHub, Visual Studio Team Services, vb.) denetleyin ve güncelleştirme hello `repo` değişken, hello şablon hello Azure işlevi da dağıtır.

### <a name="creating-an-azure-function-project"></a>Bir Azure işlevi projesi oluşturma

JavaScript, Python, F #, Bash, toplu veya PowerShell kullanarak, hello izleyin. [hello işlevleri CLI adımları](../azure-functions/functions-run-local.md) toocreate bir proje.  Bir işlev C# geliştirme, kullanabileceğiniz bir [C# sınıf kitaplığı](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) hello Azure işlevi için hello geçerli çözümde.

## <a name="next-steps"></a>Sonraki adımlar

* [Bilgi nasıl toobuild sunucusuz bir Sosyal Panosu](logic-apps-scenario-social-serverless.md)
* [Visual Studio bulut Gezgini'nden bir mantıksal uygulama yönetme](logic-apps-manage-from-vs.md)
* [Mantıksal uygulama iş akışı tanımlama dili](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
