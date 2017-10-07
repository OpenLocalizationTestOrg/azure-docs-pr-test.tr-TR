---
title: "aaaHandle bulut hizmeti yaşam döngüsü olayları | Microsoft Docs"
description: "Bir bulut hizmeti rolü hello yaşam döngüsü yöntemlerini .NET içinde nasıl kullanılacağını öğrenin"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 39b30acd-57b9-48b7-a7c4-40ea3430e451
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: cc0ccc5f055b965202b6e081a6ab72ad5d39b034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-lifecycle-of-a-web-or-worker-role-in-net"></a>Merhaba .NET Web veya çalışan rolünde ömrünü özelleştirme
Çalışan rolü oluşturduğunuzda, hello genişletmek [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) yanıt toolifecycle olayları için izin toooverride yöntemleri sağlayan sınıf. Toorespond toolifecycle olayları kullanmalısınız web rolleri için bu sınıf isteğe bağlıdır.

## <a name="extend-hello-roleentrypoint-class"></a>Merhaba RoleEntryPoint sınıfını genişletir
Hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) sınıfı, Azure tarafından çağrılan yöntemler içerir, bunu **başlatır**, **çalıştıran**, veya **durdurur** web veya çalışan rolü. İsteğe bağlı olarak, bu yöntemleri toomanage rol başlatma, rol kapatma dizileri veya hello yürütme iş parçacığı hello rolünün kılabilirsiniz. 

Genişletirken **RoleEntryPoint**, hello yöntemleri davranışlarını aşağıdaki Merhaba bilincinde olmanız gerekir:

* Merhaba [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) ve [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) yöntemleri olası tooreturn olacak şekilde bir Boole değeri döndürür **false** bu yöntemlerden.
  
   Kodunuzu döndürürse **false**hello rol işlem beklenmedik şekilde sona erdirildi, tüm kapatma dizisi çalıştırmadan yerinde olabilir. Genel olarak, döndürme kaçınmalısınız **false** hello gelen **OnStart** yöntemi.
* Herhangi bir aşırı yüklemesini içinde özel durum yakalanmamış bir **RoleEntryPoint** yöntemi, işlenmeyen bir özel durum değerlendirilir.
  
   Merhaba yaşam döngüsü yöntemlerden birini içinde bir özel durum oluşursa, Azure hello oluşturacağı [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) olay, ve ardından hello işlemi sonlandırdı. Rolünüze çevrimdışı alındıktan sonra Azure tarafından başlatılır. İşlenmeyen bir özel durum oluştuğunda, hello [durdurma](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) olay başlatılmaz ve hello **OnStop** yöntemi çağrılmaz.

Rolünüze başlamıyor ya da hello arasında meşgul ve durduruluyor durumlarını, başlatma, geri dönüştürme kodunuzun her zaman hello rolü yeniden hello yaşam döngüsü olayları biri içinde işlenmeyen bir özel durum atma. Bu durumda, hello kullanarak [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) olay toodetermine hello hello özel durumun nedeni olan ve uygun şekilde işlemesine. Rolünüze de hello döndürme [çalıştırmak](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) hello rol toorestart neden yöntemi. Dağıtım durumları hakkında daha fazla bilgi için bkz: [ortak sorunları neden rolleri tooRecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

> [!NOTE]
> Merhaba kullanıyorsanız **Azure Araçları için Microsoft Visual Studio** toodevelop, uygulamanızın hello rol proje şablonlarını otomatik olarak hello genişletmek **RoleEntryPoint** hello siziniçinsınıfında*WebRole.cs* ve *WorkerRole.cs* dosyaları.
> 
> 

## <a name="onstart-method"></a>OnStart yöntemi
Merhaba **OnStart** rol örneğinizi Azure tarafından çevrimiçi duruma getirildiğinde yöntemi çağrılır. Merhaba OnStart kod yürütülürken hello rol örneği olarak işaretlenmiş **meşgul** ve hiçbir harici trafik hello yük dengeleyici tarafından yönlendirilen tooit olacaktır. Olay işleyicileri uygulama ve başlatma gibi bu yöntemi tooperform başlatma işi, kılabilirsiniz [Azure tanılama](cloud-services-how-to-monitor.md).

Varsa **OnStart** döndürür **true**hello örneği başarıyla başlatıldı ve Azure çağırır hello **RoleEntryPoint.Run** yöntemi. Varsa **OnStart** döndürür **yanlış**, herhangi bir planlı kapatma dizisini çalıştırmadan hello rol hemen sonlandırır.

Kod örnekteki nasıl aşağıdaki hello toooverride hello **OnStart** yöntemi. Bu yöntem yapılandırır ve hello rol örneğini başlatır ve veri tooa depolama hesabı günlüğü'nün aktarma ayarlar tanı İzleyicisi başlar:

```csharp
public override bool OnStart()
{
    var config = DiagnosticMonitor.GetDefaultInitialConfiguration();

    config.DiagnosticInfrastructureLogs.ScheduledTransferLogLevelFilter = LogLevel.Error;
    config.DiagnosticInfrastructureLogs.ScheduledTransferPeriod = TimeSpan.FromMinutes(5);

    DiagnosticMonitor.Start("DiagnosticsConnectionString", config);

    return true;
}
```

## <a name="onstop-method"></a>OnStop yöntemi
Merhaba **OnStop** yöntemi, bir rol örneği Azure tarafından ve çıkılıyor hello önce çevrimdışı alındıktan sonra çağrılır. Bu yöntemi toocall kodu kapatmak, rol örneği toocleanly için gerekli kılabilirsiniz.

> [!IMPORTANT]
> Hello çalışan kodu **OnStop** yöntemi nedeniyle kullanıcı tarafından başlatılan bir kapatma dışında çağrıldığında sınırlı bir süre toofinish sahiptir. Bu süre geçtikten sonra bu kodu hello olmanız gerekir böylece hello işlemin, sonlandırıldığından **OnStop** yöntemi çalışmıyor toocompletion göstereceği veya hızlı bir şekilde çalıştırabilirsiniz. Merhaba **OnStop** yöntemi çağrıldıktan sonra hello **durdurma** olayı oluşturulur.
> 
> 

## <a name="run-method"></a>Run yöntemi
Merhaba kılabilirsiniz **çalıştırmak** yöntemi tooimplement rol örneği için uzun süre çalışan iş parçacığı.

Merhaba geçersiz kılma **çalıştırmak** yöntemi gerekli değildir; hello varsayılan uygulaması sonsuza kadar uyku bir iş parçacığı başlatır. Merhaba geçersiz kılarsanız **çalıştırmak** yöntemi, kodunuzu engelleme süresiz olarak. Merhaba, **çalıştırmak** yöntemi döndürür, hello rolü otomatik olarak düzgün bir şekilde geri dönüştürüldüğünde; diğer bir deyişle, Azure başlatır hello **durdurma** olay ve çağrıları hello **OnStop** yöntemi için kapatma dizileriniz hello rolü önce yürütülebilecek çevrimdışı hale getirilir.

### <a name="implementing-hello-aspnet-lifecycle-methods-for-a-web-role"></a>Web rolü için uygulama hello ASP.NET yaşam döngüsü yöntemleri
Ayrıca toothose hello tarafından sağlanan hello ASP.NET yaşam döngüsü yöntemleri kullanabilirsiniz **RoleEntryPoint** sınıfı, bir web rolü için toomanage başlatma ve kapatma serileri. Mevcut bir ASP.NET uygulaması tooAzure bağlantı noktası oluşturma, bu uyumluluk amacıyla yararlı olabilir. Merhaba ASP.NET yaşam döngüsü yöntemleri hello içinde çağrılır **RoleEntryPoint** yöntemleri. Merhaba **uygulama\_Başlat** yöntemi çağrıldıktan sonra hello **RoleEntryPoint.OnStart** yöntemini çağırır. Merhaba **uygulama\_son** yöntemi çağrılmadan önce hello **RoleEntryPoint.OnStop** yöntemi çağrılır.

## <a name="next-steps"></a>Sonraki adımlar
Nasıl çok öğrenin[bir bulut hizmet paketi oluşturma](cloud-services-model-and-package.md).

