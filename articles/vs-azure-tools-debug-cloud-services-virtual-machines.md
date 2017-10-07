---
title: aaaDebugging bir Azure bulut hizmeti ya da sanal makineye Visual Studio'da | Microsoft Docs
description: "Bir bulut hizmeti ya da sanal makine Visual Studio'da hata ayıklama"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 945e06e0-2100-41af-b218-72347367ddab
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 32a326430021ba2ea9317a6a71fa005d4b87c273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-an-azure-cloud-service-or-virtual-machine-in-visual-studio"></a>Bir Azure bulut hizmeti ya da sanal makineye Visual Studio'da hata ayıklama
Visual Studio Azure bulut Hizmetleri ve sanal makineleri hata ayıklama için farklı seçenekler sunar.

## <a name="debug-your-cloud-service-on-your-local-computer"></a>Bulut hizmetinizi yerel bilgisayarınızda hata ayıklama
Zaman ve para hello Azure işlem öykünücüsü toodebug kullanarak bulut hizmetinizi yerel makinede kaydedebilirsiniz. Dağıtmadan önce bir hizmet yerel olarak hata ayıklama tarafından, güvenilirlik ve performans işlem zaman için ödeme olmadan artırabilir. Ancak, bazı hatalar yalnızca bir bulut hizmeti Azure'da çalıştırdığınızda oluşabilecek kendisi. Hizmetinizi yayımlama ve hello hata ayıklayıcı tooa rol örneği attach uzaktan hata ayıklama etkinleştirirseniz, bu hatalarını ayıklayabilirsiniz.

Merhaba öykünücüsü hello Azure işlem hizmeti taklit eder ve böylece test ve dağıtmadan önce bulut hizmetinde hata ayıklama, yerel ortamınızda çalıştırır. Merhaba öykünücüsü tanıtıcıları rolü örneklerinizi yaşam döngüsü hello ve yerel depolama gibi toosimulated kaynaklarına erişim sağlar. Hata ayıklama veya hizmetinizi Visual Studio'dan çalıştırdığınızda hello öykünücüsü arka planda otomatik olarak başlar ve ardından hizmeti toohello öykünücüsü dağıtır. Merhaba yerel ortamında çalıştığında hizmetinizi hello öykünücüsü tooview kullanabilirsiniz. Merhaba tam hello express sürümünü veya hello öykünücüsü çalıştırabilirsiniz. (Azure 2.3 ile başlayarak, hello express hello öykünücüsünü hello varsayılan sürümdür.) Bkz: [Emulator Express kullanarak tooRun ve bir bulut hizmeti yerel olarak hata ayıklama](https://msdn.microsoft.com/library/dn339018.aspx).

### <a name="toodebug-your-cloud-service-on-your-local-computer"></a>Bulut hizmeti, yerel bilgisayarınızda toodebug
1. Merhaba menü çubuğunda seçin **hata ayıklama**, **hata ayıklamayı Başlat** toorun Azure bulut hizmeti projenizi. Alternatif olarak, F5 tuşuna basın. İşlem öykünücüsü hello bir ileti başlangıç görürsünüz. Merhaba öykünücüsü başladığında hello sistem tepsisi simgesi, onaylar.

    ![Merhaba sistem tepsisindeki Azure öykünücüsü](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC783828.png)
2. Görüntüleme hello kullanıcı arabirimi için hello işlem öykünücüsü hello bildirim alanında hello Azure simgesi hello kısayol menüsünü açarak ve ardından **Göster işlem öykünücüsü kullanıcı Arabiriminde**.

    şu anda hello services her hizmetinin çalıştığını toohello işlem öykünücüsü ve hello rol örnekleri dağıtılan hello UI Hello sol bölmesinde gösterir. Merhaba sağ bölmede hello hizmet ya da roller toodisplay yaşam döngüsü, günlüğe kaydetme ve tanılama bilgileri seçebilirsiniz. Merhaba üst kenar boşluğu dahil penceresinin içinde hello odak yerleştirirseniz toofill hello sağ bölmede genişletir.
3. Merhaba komutlarını seçerek adım hello uygulaması aracılığıyla **hata ayıklama** menü ve kodunda kesme noktalarını ayarlama. Merhaba uygulaması hello hata ayıklayıcısında adım adım gibi hello bölmeler hello geçerli durumunu Merhaba uygulaması ile güncelleştirilir. Hata ayıklama durdurduğunuzda, hello uygulama dağıtımı silinir. Uygulamanızı bir web rolü içerir ve hello başlangıç eylemi özellik toostart hello web tarayıcısı ayarladınız, Visual Studio web uygulamanızı hello tarayıcıda başlatır. Merhaba hello hizmet yapılandırmasında bir rol örneklerinin sayısını değiştirirseniz, bulut hizmetini durdurmak ve ardından bu yeni hello rol örneklerini ayıklayabilirsiniz böylece hata ayıklama yeniden başlatmanız gerekir.

    **Not:** olmayan ne zaman çalışmasını durdurabilir veya yerel işlem öykünücüsü ve depolama öykünücüsü hizmetiniz, hata ayıklama hello durduruldu. Bunları açıkça hello bildirim alanından durdurmanız gerekir.

## <a name="debug-a-cloud-service-in-azure"></a>Azure bulut hizmetinde hata ayıklama
Böylece gerekli Hizmetleri (örneğin, msvsmon.exe) hello sanal makinelerde çalışan rolü örneklerinizi yüklü olduğundan, bulut hizmetinizin dağıttığınızda toodebug bir bulut hizmeti uzak makinede, bu işlevselliği, açıkça etkinleştirmelisiniz. Merhaba hizmet yayımlandığında uzaktan hata ayıklamayı etkinleştirme alamadık, uzaktan hata ayıklama etkin durumdayken toorepublish hello hizmeti sahip.

Uzaktan hata ayıklama için bir bulut hizmeti etkinleştirirseniz, performans sergiler veya ek ücrete tabi değildir. Merhaba hizmeti kullanan istemciler olumsuz yönde etkilenebilir nedeniyle bir üretim hizmette uzaktan hata ayıklama kullanmamalısınız.

> [!NOTE]
> Bir bulut hizmeti Visual Studio'dan yayımladığınızda, etkinleştirebilirsiniz **IntelliTrace** söz herhangi bir rol hizmeti, hedef hello .NET Framework 4 veya .NET Framework 4.5 hello. Kullanarak **IntelliTrace**, hello son rol örneğinde oluşan olaylarla inceleyin ve bu süre hello bağlamından yeniden oluşturun. Bkz: [yayımlanan bulut hizmeti IntelliTrace ve Visual Studio ile hata ayıklama](http://go.microsoft.com/fwlink/?LinkID=623016) ve [kullanarak IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx).
>
>

### <a name="tooenable-remote-debugging-for-a-cloud-service"></a>Uzaktan hata ayıklama için bir bulut hizmeti tooenable
1. Hello Azure projesi için hello kısayol menüsünü açın ve ardından **Yayımla**.
2. Select hello **hazırlama** ortamı ve hello **hata ayıklama** yapılandırma.

    Bu yalnızca bir kılavuz olarak sağlanmıştır. Bir üretim ortamında test ortamınızı toorun tercih edebilirsiniz. Ancak, hello üretim ortamına uzaktan hata ayıklama devre dışı bırakırsanız kullanıcılar olumsuz yönde etkileyebilir. Merhaba yayın yapılandırma seçebilirsiniz, ancak daha kolay hata ayıklama hello hata ayıklama yapılandırmasını sağlar.

    ![Merhaba hata ayıklama yapılandırmasını seçin](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746717.gif)
3. Select hello ancak Hello normal adımları izleyin **etkinleştirmek uzaktan hata ayıklayıcı tüm rolleri için** hello onay kutusunu **Gelişmiş ayarları** sekmesi.

    ![Hata ayıklama yapılandırması](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746718.gif)

### <a name="tooattach-hello-debugger-tooa-cloud-service-in-azure"></a>Azure'daki tooattach hello hata ayıklayıcı tooa bulut hizmeti
1. Sunucu Gezgini'nde, bulut hizmetinizin hello düğümünü genişletin.
2. Merhaba rol veya tooattach istediğiniz ve ardından rol örneği toowhich için açık hello kısayol menüsü **Attach hata ayıklayıcı**.

    Bir rolü hata ayıklama, hello Visual Studio hata ayıklayıcısı tooeach bu rol örneği ekler. Merhaba hata ayıklayıcı kod satırını çalıştırır ve bu kesme noktası tüm koşulları karşılayan hello ilk rol örneği için bir kesme noktası kesintiye uğrar. Bir örneği hata ayıklama, hello hata ayıklayıcı örneği ve yalnızca bu belirli örnek kod satırını çalıştırır ve karşılayan bir kesme noktası sayfasındaki sonlarını kesme'nın koşullar hello tooonly ekler.

    ![Hata ayıklayıcıyı Ekle](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746719.gif)
3. Merhaba hata ayıklayıcı tooan örneği ekler sonra her zamanki gibi hata ayıklama. Merhaba hata ayıklayıcı toohello uygun ana bilgisayar işlemi rolünüz için otomatik olarak ekler. Bağlı olarak hangi hello rolüdür hello hata ayıklayıcı ekler toow3wp.exe, WaWorkerHost.exe veya WaIISHost.exe. tooverify hello işlem toowhich hello hata ayıklayıcısı ekli, Sunucu Gezgininde hello örneği düğümünü genişletin. Bkz: [Azure rol mimarisi](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) Azure işlemleri hakkında daha fazla bilgi.

    ![Kod türünü seç iletişim kutusu](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
4. tooidentify hello işlemleri toowhich hello hata ayıklayıcısı ekli, Itanium tabanlı sistemler için hello işlemleri iletişim kutusu tarafından çubuk, hata ayıklama, Windows, işlemleri seçme hello menüsünde açın. (Klavye: Ctrl + Alt + Z) toodetach belirli bir işlemin kısayol menüsünü açın ve ardından **ayırma işlemi**. Veya, hello örneği düğümü Sunucu Gezgini hello işlem bulunamadı, kısayol menüsünü açın ve ardından **ayırma işlemi**.

    ![Hata ayıklama işlemleri](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC690787.gif)

> [!WARNING]
> Kesme noktaları uzak uzun durur kaçının hata ayıklama. Azure yanıt olarak birkaç dakikadan uzun süre için durduruldu ve trafik toothat örneği gönderme durdurur işlem değerlendirir. Uzun süre durdurursanız msvsmon.exe hello işleminden ayırır.
>
>

örneği veya rol, hatalarını ayıkladığınız ve ardından hello rol veya örnek için açık hello kısayol menüsü tüm işlemler toodetach hello debugger **Detach hata ayıklayıcı**.

## <a name="limitations-of-remote-debugging-in-azure"></a>Azure'da uzaktan hata ayıklama sınırlamaları
Azure SDK 2.3 uzaktan hata ayıklama sınırlamaları aşağıdaki hello sahiptir.

* Uzaktan hata ayıklama etkin durumdayken, herhangi bir rolü 25'ten fazla örneğe sahip bir bulut hizmeti yayımlanamıyor.
* Merhaba hata ayıklayıcı bağlantı noktaları 30400 too30424, 31400 too31424 ve 32400 too32424 kullanır. Bu bağlantı noktaları hiçbirini toouse çalışırsanız, hizmetiniz ve hello aşağıdaki hata iletilerinden birini hello etkinlik günlüğünde Azure için görünür mümkün toopublish olmayacaktır:

  * Merhaba .csdef dosyası Hello .cscfg dosyasında doğrulanırken bir hata oluştu.
    Merhaba bağlantı noktası aralığı 'range' role 'rolünün' Microsoft.WindowsAzure.Plugins.RemoteDebugger.Connector bir zaten tanımlı bir bağlantı veya aralığı çakışıyor uç noktası için ayrılmış.
  * Ayırma başarısız oldu. Lütfen daha sonra yeniden deneyin, hello VM boyutu veya rol örneklerinin sayısını azaltmayı deneyin veya tooa farklı bir bölgeye dağıtmayı deneyin.

## <a name="debugging-azure-virtual-machines"></a>Hata ayıklama Azure sanal makineler
Visual Studio'da Sunucu Gezgini kullanarak Azure sanal makinelerde çalışan programlar ayıklayabilirsiniz. Bir Azure sanal makinesi üzerinde uzaktan hata ayıklama etkinleştirdiğinizde, Azure hello uzaktan hata ayıklama uzantısı hello sanal makineye yükler. Ardından, tooprocesses hello sanal makineye ekleyin ve normal olarak hata ayıklama.

> [!NOTE]
> Hello Azure Kaynak Yöneticisi yığınından oluşturulan sanal makineleri uzaktan Visual Studio 2015'te bulut Gezgini'ni kullanarak hata ayıklaması yapılabilir. Daha fazla bilgi için bkz: [bulut Gezgini ile Azure kaynaklarını yönetme](http://go.microsoft.com/fwlink/?LinkId=623031).
>
>

### <a name="toodebug-an-azure-virtual-machine"></a>toodebug bir Azure sanal makinesi
1. Sunucu Gezgini'nde, hello sanal makineler ve hello sanal makinenin toodebug istediğiniz select hello düğümlerini genişletin.
2. Merhaba bağlam menüsünü açın ve seçin **etkinleştirmek hata ayıklama**. Tooenable hello bir sanal makineyi seçin hata ayıklama istiyorsanız emin olup olmadığınız sorulduğunda **Evet**.

    Azure hello sanal makine tooenable hata ayıklamayı hello uzaktan hata ayıklama uzantısı yükler.

    ![Sanal makine hata ayıklamayı etkinleştir komutu](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Azure etkinlik günlüğü](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
3. Merhaba uzaktan hata ayıklama uzantısı Yükleme bittikten sonra hello sanal makinenin bağlam menüsünü açın ve seçin **hata ayıklayıcı Ekle...**

    Azure hello sanal makinede hello işlemlerin bir listesini alır ve bunları hello Attach tooProcess iletişim kutusunda gösterir.

    ![Hata ayıklayıcısı Ekle komutu](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
4. Merhaba, **tooProcess Attach** iletişim kutusunda **seçin** toolimit hello sonuçlar listesinde hello türleri yalnızca tooshow toodebug istediğiniz kodu. 32 veya 64-yönetilen bit kod, yerel kod veya her ikisini ayıklayabilirsiniz.

    ![Kod türünü seç iletişim kutusu](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
5. Merhaba sanal makineye toodebug istediğiniz ve ardından hello işlemleri seçin **Attach**. Örneğin, toodebug hello sanal makine üzerinde bir web uygulaması istediyseniz hello w3wp.exe işlemi seçebilirsiniz. Bkz: [hata ayıklama bir veya daha fazla işlemleri Visual Studio'da](https://msdn.microsoft.com/library/jj919165.aspx) ve [Azure rol mimarisi](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) daha fazla bilgi için.

## <a name="create-a-web-project-and-a-virtual-machine-for-debugging"></a>Bir web projesi ve hata ayıklama için bir sanal makine oluşturma
Azure projenizi yayımlamadan önce onu yararlı tootest bulabilirsiniz, hata ayıklama ve test senaryoları destekler ve yükleyebileceğiniz sınama ve programları izleme kapsanan bir ortamda. Tek yönlü toodo budur tooremotely uygulamanızı bir sanal makinede hata ayıklama.

Visual Studio ASP.NET projeleri uygulama test etmek için kullanabileceğiniz yararlı bir sanal makine bir seçenek toocreate sunar. Merhaba sanal makine PowerShell, Uzak Masaüstü'nü ve WebDeploy gibi sık gerekli uç noktaları içerir.

### <a name="toocreate-a-web-project-and-a-virtual-machine-for-debugging"></a>toocreate bir web projesi ve hata ayıklama için bir sanal makine
1. Visual Studio'da yeni bir ASP.NET Web uygulaması oluşturun.
2. Merhaba yeni ASP.NET projesi iletişim kutusunda, hello Azure bölümü seçin **sanal makine** hello açılır liste kutusunda. Merhaba bırakın **uzak kaynaklar Oluştur** onay kutusu seçili. Seçin **Tamam** tooproceed.

    Merhaba **Azure'da sanal makine oluşturma** iletişim kutusu görüntülenir.

    ![ASP.NET web projesi oluştur iletişim kutusu](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746723.png)

    **Not:** zaten oturum açtıysanız tooyour Azure hesabı toosign istenir.

1. Merhaba sanal makine için çeşitli ayarları hello seçip ardından **Tamam**. Bkz: [sanal makineleri](http://go.microsoft.com/fwlink/?LinkId=623033) daha fazla bilgi için.

    Merhaba adı için DNS adını girin, hello hello sanal makinenin adını olacaktır.

    ![Sanal makine oluştur Azure iletişim kutusu](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746724.png)

    Azure hello sanal makine ile birlikte oluşturur ve Uzak Masaüstü'nü ve Web dağıtımı gibi hello uç noktaları yapılandırır
2. Merhaba sanal makine tam olarak yapılandırıldıktan sonra sunucu Gezgini'nde hello sanal makinenin düğümünü seçin.
3. Merhaba bağlam menüsünü açın ve seçin **etkinleştirmek hata ayıklama**. Tooenable hello bir sanal makineyi seçin hata ayıklama istiyorsanız emin olup olmadığınız sorulduğunda **Evet**.

    Azure hello uzaktan hata ayıklama uzantısı toohello sanal makine tooenable hata ayıklama yükler.

    ![Sanal makine hata ayıklamayı etkinleştir komutu](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Azure etkinlik günlüğü](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
4. Kısmında özetlendiği gibi projenizin Yayımla [nasıl yapılır: bir Web projesi kullanarak tek tıklamayla yayımlama Visual Studio'da dağıtmak](https://msdn.microsoft.com/library/dd465337.aspx). Merhaba üzerindeki hello sanal makinede toodebug istediklerinden **ayarları** hello sayfasının **Web'i Yayımla** seçin **hata ayıklama** hello yapılandırma olarak. Bu hata ayıklarken kod semboller kullanılabilir olduğundan emin olur.

    ![Yayımlama ayarları](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718349.png)
5. Merhaba, **dosya yayımlama seçeneği**seçin **hedefteki ek dosyaları Kaldır** hello proje daha erken bir zamanda zaten dağıtıldıysa.
6. Sunucu Gezgininde hello sanal makinenin bağlam menüsünde Merhaba projeyi yayımlar sonra seçin **hata ayıklayıcı Ekle...**

    Azure hello sanal makinede hello işlemlerin bir listesini alır ve bunları hello Attach tooProcess iletişim kutusunda gösterir.

    ![Hata ayıklayıcısı Ekle komutu](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
7. Merhaba, **tooProcess Attach** iletişim kutusunda **seçin** toolimit hello sonuçlar listesinde hello türleri yalnızca tooshow toodebug istediğiniz kodu. 32 veya 64-yönetilen bit kod, yerel kod veya her ikisini ayıklayabilirsiniz.

    ![Kod türünü seç iletişim kutusu](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
8. Merhaba sanal makineye toodebug istediğiniz ve ardından hello işlemleri seçin **Attach**. Örneğin, toodebug hello sanal makine üzerinde bir web uygulaması istediyseniz hello w3wp.exe işlemi seçebilirsiniz. Bkz: [hata ayıklama bir veya daha fazla işlemleri Visual Studio'da](https://msdn.microsoft.com/library/jj919165.aspx) daha fazla bilgi için.

## <a name="next-steps"></a>Sonraki adımlar
* Kullanım **IntelliTrace** toocollect günlük çağrıları ve yayın sunucusundan olayları. Bkz: [yayımlanan bulut hizmeti IntelliTrace ve Visual Studio ile hata ayıklama](http://go.microsoft.com/fwlink/?LinkID=623016).
* Kullanım **Azure tanılama** toolog ayrıntılı bilgileri rolleri, kod çalıştırılmasını hello rolleri hello geliştirme ortamında veya Azure çalıştırıp çalıştırmadığınızı. Bkz: [Azure tanılama kullanarak günlük verileri toplama](http://go.microsoft.com/fwlink/p/?LinkId=400450).
