---
title: "aaaHow tooupgrade projeleri toohello geçerli sürümü hello Azure Araçları | Microsoft Docs"
description: "Nasıl tooupgrade bir Azure projesi Visual Studio toohello geçerli sürümünde hello Azure Araçları öğrenin"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1d64070a-078d-468a-87f4-e6715de6475f
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: c89ba43af0f2fd9db46ce0c90f0da3d70dc1510b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupgrade-projects-toohello-current-version-of-hello-azure-tools-for-visual-studio"></a>Tooupgrade toohello geçerli sürümü hello Azure Araçları, Visual Studio için nasıl projeleri
## <a name="overview"></a>Genel Bakış
Merhaba sürümü geçerli hello Azure Araçlar (veya 1.6 yeniyse önceki bir sürümü) yükledikten sonra Azure Araçları kullanılarak oluşturulan herhangi bir projeyle 1.6 önce sürüm (Kasım 2011) otomatik olarak yükseltilecek açmadan hemen sonra. Kullanarak projeleri oluşturduysanız bu araçları 1.6 (Kasım 2011) sürümü Merhaba ve hala bu sürümü yüklü, bu projeleri hello eski sürümde açın ve daha sonra karar olup olmadığını tooupgrade bunları.

## <a name="how-your-project-changes-when-you-upgrade-it"></a>Bu yükseltme yaptığınızda, projenizin nasıl değiştiğini
Bir proje otomatik olarak yükseltilir veya, belirtirseniz Bu, projenizin tooupgrade toowork belirli derlemeleri geçerli sürümleriyle değiştirilebilir ve bu bölümde açıklandığı gibi bazı özellikler da değiştirilir istiyorsunuz. Projenizi hello yeni hello araçları sürümüyle uyumlu diğer değişiklikleri toobe gerektiriyorsa, bu değişiklikleri el ile yapmalısınız.

* Merhaba web.config dosyası web rolleri için ve çalışan rolleri için hello app.config dosyası güncelleştirilmiş tooreference hello daha yeni sürümü Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll var.
* Merhaba Microsoft.WindowsAzure.StorageClient.dll, Microsoft.WindowsAzure.Diagnostics.dll ve Microsoft.WindowsAzure.ServiceRuntime.dll derlemeler yükseltilmiş toohello yeni sürümleri.
* Hello Azure proje dosyası (.ccproj) depolanan yayımlama profilleri olan hello içinde hello uzantısı .azurePubXml ile taşınan tooa ayrı dosya **Yayımla** alt dizin.
* Yayımlama hello bazı özellikleri profili güncelleştirilmiş toosupport yeni ve değiştirilmiş özellikleri verilmiştir. **AllowUpgrade** değiştirilir **DeploymentReplacementMethod** aynı anda veya artımlı olarak dağıtılan bulut hizmeti güncelleştirmek için.
* Merhaba özelliği **UseIISExpressByDefault** eklenir ve böylece hello hata ayıklama için kullanılan web sunucusu otomatik olarak Internet Information Services (IIS) tooIIS Express değişmeyeceği toofalse ayarlayın. IIS Express hello varsayılan web hello daha yeni sürümlerini hello araçları ile oluşturulmuş projelerde sunucusudur.
* Azure önbelleği bir veya daha fazla projenizin rolleri barındırılıyorsa, proje yükseltildiğinde bazı özellikler hello hizmet yapılandırma (.cscfg dosyası) ve hizmet tanımı (.csdef dosyası) değiştirilir. Merhaba proje hello Azure önbelleğe alma NuGet paketini kullanıyorsa, hello hello paketinin en son sürümüne yükseltilmiş toohello projesidir. Merhaba web.config dosyasını açın ve hello istemci yapılandırma, düzgün şekilde hello yükseltme işlemi sırasında tutulan doğrulamanız gerekir. Merhaba NuGet paketini kullanmadan hello başvuruları tooAzure önbelleğe alma istemci derlemelerine eklediyseniz, bu derlemeler güncelleştirilmez; Bu başvurular toohello yeni sürümleri el ile güncelleştirmeniz gerekir.

> [!IMPORTANT]
> F # projeleri için böylece bu derlemeler daha yeni sürümleri hello başvuru başvuruları tooAzure derlemeleri el ile güncelleştirmelisiniz.
> 
> 

### <a name="how-tooupgrade-an-azure-project-toohello-current-release"></a>Nasıl tooupgrade bir Azure projesi toohello geçerli sürüm
1. Merhaba toouse istediğiniz hello geçerli sürümünü yüklemek hello Azure Araçları Visual Studio hello yüklemesi içine proje ve ardından açık hello proje tooupgrade istediğiniz yükseltilmiştir. Hello projenizi Azure Araçları ile oluşturduysanız yayın önce 1.6 (Kasım 2011) hello proje otomatik olarak yükseltilen toohello geçerli sürümdür. Hello proje Kasım 2011 yayın hello ile oluşturulmuş ve yayın hala yüklü değilse, bu sürümde hello projesi açılır.
2. Çözüm Gezgini'nde açık hello kısayol menüsünü hello proje düğümüne seçin **özellikleri**ve ardından hello **uygulama** görünür hello iletişim kutusunda.
   
    Merhaba **uygulama** sekmesi hello projeyle ilişkili hello Araçları sürüm gösterir. Azure Araçları'nın geçerli sürümü Hello görünürse, hello proje zaten yükseltildi. Hangi hello sekmesi gösterir, daha hello araçları, yeni bir sürümünü yüklediyseniz bir **yükseltme** düğmesi görünür.
3. Merhaba seçin **yükseltme** düğmesini tooupgrade proje toohello güncel bir sürümünü hello araçları.
4. Merhaba projeyi oluşturun ve sonra API değişikliklerden kaynaklanan hataları çözün. Hakkında bilgi için toomodify kodunuz hello yeni sürümü için bkz. nasıl hello belgelerine belirli API hello.

