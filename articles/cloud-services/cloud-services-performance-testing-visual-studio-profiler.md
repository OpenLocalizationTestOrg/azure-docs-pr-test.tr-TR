---
title: "bir bulut hizmeti yerel olarak hello işlem öykünücüsü içinde aaaProfiling | Microsoft Docs"
services: cloud-services
description: "Merhaba Visual Studio Profil Oluşturucu ile bulut Hizmetleri performans sorunları araştırmak"
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a>Hello Azure işlem öykünücüsü kullanarak hello Visual Studio profil oluşturucu Hello performansını bir bulut hizmeti yerel olarak test etme
Çeşitli araçları ve teknikleri, bulut Hizmetleri hello performansını test etmek için kullanılabilir.
Bir bulut hizmeti tooAzure yayımladığınızda, Visual Studio profil oluşturma verileri toplamak ve ardından analiz olabilir açıklandığı gibi yerel olarak [bir Azure uygulama profili oluşturma][1].
De açıklandığı gibi çeşitli performans sayaçları, tanılama tootrack kullanabilirsiniz [Azure'da performans sayaçlarını kullanarak][2].
Tooprofile toohello bulut dağıtmadan önce uygulamanızda yerel olarak hello işlem öykünücüsü isteyebilirsiniz.

Bu makalede, yerel olarak hello öykünücüsünde yapılabilir profil hello CPU örnekleme yöntemi kapsar. CPU örnekleme, profil oluşturma yöntemi çok zorlayıcı değildir. Belirlenen örnekleme aralığı sırasında hello profil oluşturucu hello çağrı yığınının bir anlık görüntüsünü alır. Merhaba veriler, bir süre boyunca toplanan ve bir raporda. Profil oluşturma yöntemi, burada bir pkı'ya yoğun uygulamasında hello CPU çalışmanın çoğu yapılır tooindicate eğilimi gösterir.  Bu, uygulamanızın çoğu zaman hello yeri harcıyorsa fırsat toofocus yolunda hello"etkin" Merhaba olanağı sağlar.

## <a name="1-configure-visual-studio-for-profiling"></a>1: profil oluşturma için Visual Studio'yu yapılandırma
İlk olarak, profil oluşturma zaman yararlı olabilecek birkaç Visual Studio yapılandırma seçenekleri mevcuttur. toomake duygusu hello profil oluşturma raporları, uygulama ve ayrıca sistem kitaplıkları simgelerini simge (.pdb dosyaları) gerekir. Toomake hello kullanılabilir simge sunucuları başvuru emin isteyeceksiniz. toodo hello üzerinde bu **Araçları** Visual Studio'da menüsünü seçin **seçenekleri**, ardından **hata ayıklama**, sonra **simgeleri**. Microsoft simge sunucuları altında listelendiğini doğrulayın **simge (.pdb) dosya konumları**.  Ayrıca ek simge dosyaları olabilir http://referencesource.microsoft.com/symbols başvuruda bulunabilir.

![Sembol Seçenekleri][4]

İsterseniz, basitleştirebilir hello raporları sadece kendi kodumu ayarlayarak bu hello profil oluşturucu oluşturur. Yalnızca My etkin kodla işlevi çağrı yığınları tamamen iç toolibraries çağırır ve .NET Framework hello hello raporlardan gizli basitleştirilmiştir. Merhaba üzerinde **Araçları** menüsünde seçin **seçenekleri**. Merhaba genişletin **performans araçları** düğümünü ve **genel**. Merhaba onay kutusunu seçip **sadece kendi kodumu etkinleştir profil oluşturucu raporlar için**.

![Yalnızca kendi kodum seçenekleri][17]

Bu yönergeler, var olan bir proje veya yeni bir proje ile kullanabilirsiniz.  Aşağıda açıklanan teknikleri yeni bir proje tootry hello oluşturursanız, C# seçin **Azure bulut hizmeti** proje ve seçin bir **Web rolü** ve **çalışan rolü**.

![Azure bulut hizmeti projesi rolleri][5]

Örneğin, amaçları için çok zaman alır ve bazı bariz performans sorununu gösterir bazı kod tooyour projesi ekleyin. Örneğin, kod tooa çalışan rolü projesi aşağıdaki hello ekleyin:

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

Bu kod hello hello çalışan rolün RoleEntryPoint türetilmiş sınıf RunAsync yönteminde çağırmanıza. (Zaman uyumlu olarak çalışan hello yöntemi hakkında hello uyarıyı yok sayın.)

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

Derleme ve bulut hizmetinizi yerel olarak (Ctrl + F5) hata ayıklama olmadan hello çözüm yapılandırma çok kümesi çalıştırma**sürüm**. Bu, tüm dosya ve klasörlerin hello uygulama yerel olarak çalıştırmak için oluşturulur ve tüm hello Öykünücüler başlatıldığını sağlar sağlar. Merhaba işlem öykünücüsü kullanıcı Arabiriminde, çalışan rolü çalıştıran hello görev tooverify başlatın.

## <a name="2-attach-tooa-process"></a>2: tooa işlem ekleme
Visual Studio 2010 IDE hello başlatarak Merhaba uygulaması profil yerine, işlem çalışan hello profil oluşturucu tooa ilişkilendirmeniz gerekir. 

tooattach hello profil oluşturucu tooa işlemi, hello **Çözümle** menüsünde seçin **profil oluşturucu** ve **Attach/Detach**.

![Profil seçeneği ekleme][6]

Çalışan rolü için hello WaWorkerHost.exe işlem bulunamadı.

![WaWorkerHost işlemi][7]

Hello profil oluşturucu proje klasörünüzdeki bir ağ sürücüsündeyse, başka bir konum toosave hello profil oluşturma raporları tooprovide sorar.

 Tooa web rolü tooWaIISHost.exe ekleyerek de ekleyebilirsiniz.
Toouse hello ProcessId toodistinguish ihtiyacınız uygulamanızda birden çok rol işçi varsa, bunları. Merhaba işlem nesnesi erişerek hello ProcessId program aracılığıyla sorgulayabilirsiniz. Örneğin, bir rolde bu kodu toohello Çalıştır yöntemi hello RoleEntryPoint türetilmiş sınıf eklerseniz, hello işlem öykünücüsü kullanıcı Arabiriminde tooknow hangi işlem tooconnect günlüğüne bakabilirsiniz.

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

tooview hello günlüğü, başlangıç hello işlem öykünücüsü kullanıcı Arabiriminde.

![Merhaba işlem öykünücüsü kullanıcı arabirimini Başlat][8]

Merhaba çalışan rolü günlük konsol penceresinde hello konsol penceresinin başlık çubuğunda tıklayarak hello işlem öykünücüsü kullanıcı arabirimini açın. Merhaba işlem kimliği hello günlüğünde görebilirsiniz.

![Görünüm işlem kimliği][9]

Bir bağlı uygulamanızın (gerekirse) UI tooreproduce hello senaryoda hello adımları gerçekleştirin.

Toostop profil istediğinizde hello seçin **durdurmak profil** bağlantı.

![Seçeneği profil oluşturmayı durdurmak][10]

## <a name="3-view-performance-reports"></a>3: performans raporları görüntüleyin
Merhaba performans raporu, uygulamanız için görüntülenir.

Bu noktada, hello profil oluşturucu yürütülürken durdurur, veri .vsp dosyası olarak kaydeder ve bu verilerin analizini gösteren bir rapor görüntüler.

![Profil Oluşturucu raporu][11]

Hello String.wstrcpy görürseniz etkin yolunuzda, sadece kendi kodumu toochange hello tıklatıldığında yalnızca tooshow kullanıcı kodu görüntüleyin.  String.Concat görürseniz, hello Göster tüm kod düğmesine basarak deneyin.

Merhaba Birleştir yöntemi ve büyük bölümünü hello yürütme süresi alma String.Concat görmeniz gerekir.

![Analiz raporu][12]

Bu makalede hello dize birleştirme kod eklediyseniz, bu uyarı hello görev listesi olarak görmeniz gerekir. Oluşturulan ve atıldı dizeleri toohello sayısı çöp toplama aşırı miktarda olduğunu belirten bir uyarı da görebilirsiniz.

![Performans uyarıları][14]

## <a name="4-make-changes-and-compare-performance"></a>4: değişiklikleri yapın ve performans karşılaştırma
Merhaba performans önce ve sonra bir kod değişikliği de karşılaştırabilirsiniz.  İşlem çalışan hello durdurmak ve hello kodu tooreplace hello dize birleştirme işlemi hello kullanımıyla StringBuilder'ın düzenleyin:

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

Başka bir performans çalışma yapın ve ardından hello performans karşılaştırın. Hello performans Gezgini, hello çalıştırır hello demektir aynı oturum, yalnızca her iki raporu seçebilir, hello kısayol menüsünü açın ve seçin **karşılaştırmak performans raporları**. Başka bir performans oturumda çalıştırılan toocompare istiyorsanız hello açın **Çözümle** menüsünde ve **karşılaştırmak performans raporları**. Her iki dosya görüntülenen hello iletişim kutusunda belirtin.

![Performans raporları seçeneği Karşılaştır][15]

Merhaba raporları hello iki çalışması arasındaki farklar vurgulayın.

![Karşılaştırma raporu][16]

Tebrikler! Hello Profil Oluşturucu ile başladıktan.

## <a name="troubleshooting"></a>Sorun giderme
* Yayın derlemesi profil ve hata ayıklama olmadan Başlat emin olun.
* Hello profil oluşturucu menüsünde Hello Attach/Detach seçeneği etkin değilse hello performans Sihirbazı'nı çalıştırın.
* Merhaba işlem öykünücüsü kullanıcı Arabiriminde tooview hello uygulamanızın durumunu kullanın. 
* Uygulamaları hello öykünücüsünde başlatma ile ilgili sorunlar varsa veya hello profil oluşturucu ekleme hello işlem öykünücüsü kapatın ve yeniden başlatın. Bu hello sorunu çözmezse, yeniden başlatmayı deneyin. Merhaba işlem öykünücüsü toosuspend kullanın ve çalışan dağıtımları kaldırırsanız bu sorun oluşabilir.
* Komutları komut satırından profil oluşturma hello birini kullandıysanız, özellikle genel ayarları Merhaba, VSPerfClrEnv /globaloff çağrıldı ve VsPerfMon.exe kapatıldı emin olun.
* Örnekleme yaparken hello iletiyi görürseniz "PRF0025: Toplanan hiçbir veriler," toohas CPU etkinlik bağlı işlem hello denetleyin. Herhangi bir hesaplama iş yapmamanın uygulamaları herhangi bir örnekleme veri oluşturamayabilir.  Tüm örnekleme yapıldığı önce hello işlem çıktı mümkündür. Run yöntemi profil bir rol için hello onay toosee Sonlandır değil.

## <a name="next-steps"></a>Sonraki Adımlar
Azure ikili hello öykünücüsü dosyalarda düzenleme hello Visual Studio profil oluşturucu içinde desteklenmez, ancak tootest bellek ayırma istiyorsanız, profil olduğunda bu seçeneği seçebilirsiniz. Ayrıca eşzamanlılık profili oluşturma, iş parçacığı için kilit zaman rekabet israfı olup olmadığını belirlemek ya da katman etkileşim profil, bir uygulama katmanları arasında kullanılırken performans sorunları izlemenize yardımcı olan en yardımcı olan seçebilirsiniz sık sık hello veri katmanı ve çalışan rolü arasında.  Uygulamanızı oluşturur hello veritabanı sorgularını görüntüleyin ve veri tooimprove hello veritabanı kullanımınız profil hello kullanın. Merhaba blog gönderisi katman etkileşim profil hakkında daha fazla bilgi için bkz [izlenecek yol: Visual Studio Team System 2010 katman etkileşim profil oluşturucu hello kullanarak][3].

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
