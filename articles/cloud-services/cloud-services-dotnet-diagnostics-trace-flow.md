---
title: "Bulut Hizmetleri uygulamasıyla Azure tanılama aaaTrace hello akışı | Microsoft Docs"
description: "İzleme iletileri tooan Azure uygulamanızı toohelp hata ayıklama, performansını ölçmek, izleme, trafik analizi ve daha ekleyin."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a>Bulut Hizmetleri uygulaması Azure Tanılama ile Merhaba akışını izleme
Çalışırken izleme, toomonitor hello yürütülmesi için uygulamanızın yoludur. Merhaba kullanabilirsiniz [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), ve [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) sınıfları toorecord hatalar hakkında bilgi ve Uygulama yürütme günlükleri, metin dosyaları veya diğer cihazları daha sonra çözümlemek için. İzleme hakkında daha fazla bilgi için bkz: [izleme ve düzenleme uygulamaları](https://msdn.microsoft.com/library/zs6s4h68.aspx).

## <a name="use-trace-statements-and-trace-switches"></a>İzleme deyimleri ve izleme anahtarları kullanın
Uygulama izleme hello ekleyerek, bulut Hizmetleri uygulamanızda [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello uygulama yapılandırması ve yapma çağırır tooSystem.Diagnostics.Trace veya System.Diagnostics.Debug içinde uygulama kodu. Kullanım hello yapılandırma dosyası *app.config* çalışan roller ve hello *web.config* web rolleri için. Visual Studio şablon kullanarak yeni bir barındırılan hizmet oluşturduğunuzda, Azure tanılama toohello proje otomatik olarak eklenir ve hello DiagnosticMonitorTraceListener toohello eklediğiniz hello rolleri için uygun yapılandırma dosyası eklenir.

İzleme deyimleri yerleştirme hakkında daha fazla bilgi için bkz: [nasıl yapılır: izleme deyimleri ekleme tooApplication kod](https://msdn.microsoft.com/library/zd83saa2.aspx).

Yerleştirerek [izleme anahtarları](https://msdn.microsoft.com/library/3at424ac.aspx) kodunuzda izleme olup oluşur ve ne kadar kapsamlı olduğunu denetleyebilirsiniz. Uygulamanızı bir üretim ortamında hello durumunu izlemenize izin verir. Birden çok bilgisayar üzerinde çalışan birden çok bileşenleri kullanan bir iş uygulaması bu durum özellikle önemlidir. Daha fazla bilgi için bkz: [nasıl yapılır: izleme anahtarları yapılandırma](https://msdn.microsoft.com/library/t06xyy08.aspx).

## <a name="configure-hello-trace-listener-in-an-azure-application"></a>Bir Azure uygulamasında Hello İzleme dinleyicisi yapılandırın
İzleme, hata ayıklama ve TraceSource, "dinleyicileri" toocollect ve gönderilen kayıt Merhaba iletileri ayarlamanız gerekir. Dinleyicileri toplamak, depolamak ve izleme iletileri yönlendirebilir. Bunlar hello İzleme çıktısı tooan uygun hedef, günlük, pencere veya metin dosyası gibi doğrudan. Azure tanılama kullanan hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) sınıfı.

Aşağıdaki yordamı hello tamamlamadan önce hello Azure Tanılama izleme başlatması gerekir. toodo Bu, bkz: [Microsoft Azure tanılama etkinleştirme](cloud-services-dotnet-diagnostics.md).

Visual Studio tarafından sağlanan hello şablonları kullanırsanız, hello dinleyicisi hello yapılandırmasını otomatik olarak sizin yerinize eklendiğine dikkat edin.

### <a name="add-a-trace-listener"></a>İzleme dinleyicisi ekleme
1. Rolünüz için Hello web.config veya app.config dosyasını açın.
2. Aşağıdaki kod toohello dosyasına hello ekleyin. Başvurduğunuz hello derlemenin Hello sürüm özniteliği toouse hello sürüm numarasını değiştirin. güncelleştirmeleri tooit olmadıkça hello derleme sürümü her Azure SDK sürümüyle mutlaka değiştirmez.
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > Bir proje başvurusu toohello Microsoft.WindowsAzure.Diagnostics derleme olduğundan emin olun. Güncelleştirme hello sürüm numarası hello XML toomatch hello hello sürümü yukarıda Microsoft.WindowsAzure.Diagnostics derleme başvuruyor.
   > 
   > 
3. Merhaba yapılandırma dosyasını kaydedin.

Dinleyicileri hakkında daha fazla bilgi için bkz: [izleme dinleyicileri](https://msdn.microsoft.com/library/4y5y10s7.aspx).

Merhaba adımları tooadd hello dinleyicisi tamamladıktan sonra izleme deyimleri tooyour kodu ekleyebilirsiniz.

### <a name="tooadd-trace-statement-tooyour-code"></a>tooadd izleme deyimi tooyour kodu
1. Uygulamanız için bir kaynak dosyasını açın. Örneğin, hello <RoleName>.cs dosyası hello çalışan rolü veya web rolü.
2. Merhaba aşağıdakileri ekleyin zaten eklenemiyor deyimi kullanarak:
    ```
        using System.Diagnostics;
    ```
3. Uygulamanızı hello durumu hakkında toocapture bilgi istediğiniz yere izleme deyimleri ekleyin. Yöntemleri tooformat hello hello izleme deyimi çıktısını çeşitli kullanabilirsiniz. Daha fazla bilgi için bkz: [nasıl yapılır: izleme deyimleri ekleme tooApplication kod](https://msdn.microsoft.com/library/zd83saa2.aspx).
4. Merhaba kaynak dosyayı kaydedin.

