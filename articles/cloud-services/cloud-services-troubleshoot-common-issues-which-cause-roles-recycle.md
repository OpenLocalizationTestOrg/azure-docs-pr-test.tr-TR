---
title: "aaaCommon neden geri dönüştürülüyor bulut hizmeti rolleri | Microsoft Docs"
description: "Aniden geri dönüştürüldüğünde bir bulut hizmet rolü önemli kapalı kalma süresi neden olabilir. Geri Dönüşüm, kapalı kalma süresini azaltmanıza yardımcı olabilecek rolleri toobe neden bazı yaygın sorunlar aşağıda verilmiştir."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 8fa152b33d2b22a8a02f834d4bc38519b4272f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="common-issues-that-cause-roles-toorecycle"></a>Rolleri toorecycle neden olan yaygın sorunları
Bu makalede, bazı hello yaygın nedenlerinden biri dağıtım sorunlarını ele alır ve sorun giderme ipuçları toohelp sağlar, bu sorunları çözün. Bir sorun uygulamayla var. hello rol örneği toostart hata verdiğinde veya hello başlatılırken, meşgul ve durdurma durumları arasında geçiş yapar göstergesidir.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a>Eksik çalışma zamanı bağımlılıkları
Bir rol, uygulamanızda hello parçası olmayan herhangi bir derlemesinin üzerinde dayalıysa .NET Framework veya hello Azure yönetilen kitaplık, bu derleme hello uygulama paketinde açıkça eklemeniz gerekir. Diğer Microsoft çerçevelerinin varsayılan olarak Azure üzerinde kullanılabilir olmadığını göz önünde bulundurun. Bu tür bir Framework'te rolünüze bağlı ise, bu derlemeler toohello uygulama paketi eklemeniz gerekir.

Derleme ve uygulamanızı paket önce hello aşağıdakileri doğrulayın:

* Visual studio kullanarak, hello emin olun. **kopya yerel** özelliği çok ayarlanmış**True** her hello Azure SDK'sı bir parçası değil, projenizdeki derlemeye referans veya .NET Framework hello.
* Merhaba web.config dosyasında hello derleme öğesi kullanılmayan tüm derlemelerde başvurmuyor emin olun.
* Merhaba **yapı eylemi** her .cshtml dosyasında çok ayarlanır**içerik**. Bu hello dosyaları hello paketinde doğru görünür ve diğer başvurulan dosyaları tooappear hello paketindeki etkinleştirir sağlar.

## <a name="assembly-targets-wrong-platform"></a>Derleme hedefleri yanlış platformu
Azure 64-bit ortamıdır. Bu nedenle, .NET derleme için bir 32 bit hedef derlenmiş Azure üzerinde çalışmaz.

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a>Rol başlatma veya durdurma sırasında işlenmeyen özel durum oluşturur
Merhaba hello yöntemler tarafından oluşturulan özel durumlar [RoleEntryPoint] hello içeren sınıf [OnStart], [OnStop], ve [Çalıştır]yöntemleri, İşlenmeyen özel durumlar şunlardır. Aşağıdaki yöntemlerden birini işlenmeyen bir özel durum oluşursa, hello rol geri. Merhaba rol sürekli geri dönüştürme, işlenmeyen bir özel durum toostart her çalıştığında atma.

## <a name="role-returns-from-run-method"></a>Run yöntemi rol döndürür
Merhaba [Çalıştır] yöntemdir hedeflenen toorun süresiz olarak. Kodunuzu hello kılıyorsa [Çalıştır] , onu sleep yöntemi süresiz olarak. Merhaba, [Çalıştır] yöntemi döndürür, hello rol geri dönüştürür.

## <a name="incorrect-diagnosticsconnectionstring-setting"></a>Yanlış DiagnosticsConnectionString ayarı
Uygulama Azure tanılama kullanıyorsa, hizmet yapılandırma dosyası hello belirtmelisiniz `DiagnosticsConnectionString` yapılandırma ayarı. Bu ayar, Azure üzerinde bir HTTPS bağlantısı tooyour depolama hesabı belirtmeniz gerekir.

tooensure, sizin `DiagnosticsConnectionString` uygulama paketi tooAzure dağıtmadan önce ayarlarının doğru olduğundan, hello şunları doğrulayın:  

* Merhaba `DiagnosticsConnectionString` noktaları Azure'da tooa geçerli bir depolama hesabı ayarlama.  
  Varsayılan olarak, bu ayar, uygulama paketini dağıtmadan önce bu ayarı değiştirmek açıkça gerekir böylece benzetilmiş toohello depolama hesabı, işaret eder. Bu ayar değiştirmezseniz hello rol örneği toostart hello tanı İzleyicisi çalıştığında özel durum oluşur. Bu hello rol örneği toorecycle süresiz olarak neden olabilir.
* Merhaba bağlantı dizesi hello aşağıda belirtilen [biçimi](../storage/common/storage-configure-connection-string.md). (Merhaba Protokolü HTTPS belirtilmesi gerekir.) Değiştir *MyAccountName* depolama hesabınızın hello adla ve *MyAccountKey* erişim anahtarı ile:    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  Microsoft Visual Studio için Azure araçlarını kullanarak, uygulama geliştiriyorsanız, bu değer hello özellik sayfaları tooset kullanabilirsiniz.

## <a name="exported-certificate-does-not-include-private-key"></a>Dışarı aktarılan sertifika özel anahtar içermiyor
toorun SSL altında web rolü, dışa aktarılan yönetim sertifikanızı hello özel anahtar içerdiğinden emin olmanız gerekir. Merhaba kullanırsanız *Windows Sertifika Yöneticisi'ni* tooexport hello sertifika emin tooselect olması **Evet** hello için **verme hello özel anahtarı** seçeneği. Hello sertifika şu anda desteklenen hello yalnızca biçimi olan hello PFX biçiminde dışarı aktarılmalıdır.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi görüntülemek [sorun giderme makalelerini](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) bulut Hizmetleri için.

Daha fazla rol senaryolarında geri dönüştürme görüntülemek [Kevin Williamson'ın blog dizisini](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[Çalıştır]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx
