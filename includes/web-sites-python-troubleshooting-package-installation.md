Bazı paketler, Azure üzerinde çalıştığında pip kullanılarak yüklenemez.  Yalnızca bu hello paket Python paket dizinini hello üzerinde kullanılamıyor olabilir.  Derleyici gerekiyor olabilir (derleyici hello makine çalışan hello web uygulamasını Azure App Service mevcut değildir).

Bu bölümde, biz Bu sorun yolları toodeal göreceğiz.

### <a name="request-wheels"></a>Tekerlek isteği
Merhaba paket yükleme bir derleyici gerekiyorsa Tekerlek hello paketi için kullanılabilir hale hello paket sahibi toorequest görüşmeye çalışmalısınız.

Merhaba son kullanılabilirliği ile [Python 2.7 için Microsoft Visual C++ derleyicisi][Microsoft Visual C++ Compiler for Python 2.7], Python 2.7 için yerel koda sahip daha kolay toobuild paketleri sunulmuştur.

### <a name="build-wheels-requires-windows"></a>Tekerlek derleme (Windows gerekir)
Not: Bu seçenek kullanıldığında hello platform/mimari/hello web uygulamasını Azure App Service'te kullanılan sürümle eşleşen Python ortamı kullanılarak emin toocompile hello paket olun (Windows/32-bit/2.7 veya 3.4).

Derleyici gerektirdiğinden hello paket yüklenmediyse hello derleyici yerel makinenize yükleyin ve ardından, depoda yerini alacaktır hello paketi için bir tekerlek derleme.

Mac/Linux kullanıcıları: erişim tooa Windows makinesine sahip değilseniz, bkz: [çalıştıran sanal makine Windows oluşturma] [ Create a Virtual Machine Running Windows] nasıl toocreate Azure üzerinde bir VM.  Toobuild hello Tekerlek kullanın, toohello deposunu ekleyin ve hello VM isterseniz atın. 

Python 2.7 için yüklediğiniz [Python 2.7 için Microsoft Visual C++ derleyicisi][Microsoft Visual C++ Compiler for Python 2.7].

Python 3.4 için yüklediğiniz [Microsoft Visual C++ 2010 Express'in][Microsoft Visual C++ 2010 Express].

toobuild Tekerlek hello Tekerlek paketi gerekir:

    env\scripts\pip install wheel

Kullanacağınız `pip wheel` toocompile bir bağımlılık:

    env\scripts\pip wheel azure==0.8.4

Bu, hello \wheelhouse klasöründe bir .whl dosyası oluşturur.  Merhaba \wheelhouse klasörünü ve Tekerlek dosyalarını tooyour deposu ekleyin.

Requirements.txt tooadd hello Düzenle `--find-links` hello üst seçeneği. Bu, devam eden toohello python paket dizinini önce hello yerel klasörde tam bir eşleşme PIP toolook bildirir.

    --find-links wheelhouse
    azure==0.8.4

Tüm bağımlılıklarınızı hello \wheelhouse klasörünü ve kullanılmıyor hello python paketinde dizin hiç tooinclude istiyorsanız ekleyerek PIP tooignore hello paket dizini zorlayabilirsiniz `--no-index` requirements.txt dosyanızın en üstüne toohello.

    --no-index

### <a name="customize-installation"></a>Yüklemeyi özelleştirme
Merhaba dağıtım komut dosyası tooinstall hello sanal ortamdaki, alternatif bir yükleyici gibi kolay kullanarak bir paket özelleştirebilirsiniz\_yükleyin.  Açıklama satırı yapılan bir örnek için deploy.cmd dosyasına bakın.  Requirements.txt, bunları yüklenmesini tooprevent PIP ne gibi paketlerin listelenmediğinden emin olun.

Bu toohello dağıtım betiği ekleyin:

    env\scripts\easy_install somepackage

Kolay mümkün toouse de olabilir\_tooinstall bir exe Yükleyiciden yükleme (zip uyumludur; bu nedenle easy bazılarıdır\_install bunları destekler).  Merhaba yükleyici tooyour deposunu ekleyin ve kolay çağırma\_hello yolu toohello yürütülebilir geçirerek yükleyin.

Bu toohello dağıtım betiği ekleyin:

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a>Merhaba sanal ortamı (Windows gerekir) hello depoya ekleme
Not: Bu seçenek kullanıldığında emin toouse hello platform/mimari/hello web uygulamasını Azure App Service'te kullanılan sürümle eşleşen sanal bir ortama olun (Windows/32-bit/2.7 veya 3.4).

Merhaba sanal ortam hello depoya eklerseniz, hello dağıtım komut dosyası boş bir dosya oluşturarak azure'da sanal ortamı yönetimi gerçekleştirmesine engel olabilirsiniz:

    .skipPythonDeployment

Merhaba sanal ortam otomatik olarak yönetildiğinde var olan sanal ortamı hello uygulama, tooprevent kalan dosyalarından hello silme öneririz.

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
