Azure, uygulamanızın **bu koşulların her ikisi de doğruysa** Python kullandığını saptayacaktır:

* Requirements.txt dosyası hello kök klasöründe
* hello kök klasöründe tüm .py dosyaları veya python belirten runtime.txt

Hello durum böyle olduğunda, hello gibi ek Python işlemlerinin yanı sıra dosyaların standart eşitlemesini gerçekleştiren bir Python belirli bir dağıtım betik kullanacaksınız:

* Sanal ortamın otomatik yönetimi
* PIP kullanarak requirements.txt dosyasında listelenen paketlerin yüklenmesi
* Seçili Python versiyonunu hello üzerinde temel hello uygun web.config oluşturma.
* Django uygulamaları için statik dosyaları toplama

Toocustomize hello betik gerek kalmadan hello varsayılan dağıtım adımları belirli yönlerini kontrol edebilir.

Tüm Python'a özel dağıtım adımlarını tooskip istiyorsanız bu boş dosyayı oluşturabilirsiniz:

    \.skipPythonDeployment

Django uygulamanız için statik dosya tooskip koleksiyonunu istiyorsanız:

    \.skipDjango 

Dağıtım üzerinde daha fazla denetim için aşağıdaki dosyaları hello oluşturarak hello varsayılan dağıtım betiğini geçersiz kılabilirsiniz:

    \.deployment
    \deploy.cmd

Merhaba kullanabilirsiniz [Azure komut satırı arabirimi] [ Azure command-line interface] toocreate hello dosyaları.  Bu komutu proje klasörünüzden kullanın:

    azure site deploymentscript --python

Bu dosyalar olmadığında, Azure geçici bir dağıtım betiği oluşturur ve bunu çalıştırır.  Bir oluşturduğunuz yukarıdaki hello komutu ile aynı toohello olur.

[Azure command-line interface]: http://azure.microsoft.com/downloads/
