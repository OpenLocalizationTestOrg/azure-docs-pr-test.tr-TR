---
title: "Azure Machine Learning deneme hizmeti yapılandırma dosyaları"
description: "Bu belgede Azure ML deneme hizmeti için yapılandırma ayarlarını ayrıntılarını verir."
services: machine-learning
author: gokhanuluderya-msft
ms.author: gokhanu
manager: haining
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 09/28/2017
ms.openlocfilehash: 16c72f8c22307a124fdb670aabca771084c0d1ec
ms.sourcegitcommit: a48e503fce6d51c7915dd23b4de14a91dd0337d8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/05/2017
---
# <a name="azure-machine-learning-experimentation-service-configuration-files"></a>Azure Machine Learning deneme hizmeti yapılandırma dosyaları

Azure Machine Learning (Azure ML) çalışma ekranı bir komut çalıştırdığınızda yürütme davranışını dosyalarında denetlenir **aml_config** klasör. Bu klasör, proje klasörünü kök altında bulunur. İstenen sonuca, yürütme için bir en iyi şekilde yararlanmak için bu dosyaların içeriğini anlamak önemlidir.

Bu klasör altındaki ilgili dosyalar şunlardır:
- conda_dependencies.yml
- spark_dependencies.yml
- hedef dosyalar işlem
    - \<Hedef adı işlem > .compute
- yapılandırma dosyalarını çalıştır
    - \<Yapılandırma adı Çalıştır > .runconfig

>[!NOTE]
>Genellikle bir işlem hedef dosya varsa ve oluşturduğunuz her işlem hedef için yapılandırma dosyasını çalıştırın. Ancak, bu dosyaları bağımsız olarak oluşturmak ve aynı işlem hedef noktası birden çok çalışma yapılandırma dosyalarının sahip.

## <a name="condadependenciesyml"></a>conda_dependencies.yml
Bu dosya bir [conda ortam dosya](https://conda.io/docs/using/envs.html#create-environment-file-by-hand) kodunuzu bağımlı paketler ve Python çalışma zamanı sürümü belirtir. Azure ML çalışma ekranı bir Docker kapsayıcısı veya Hdınsight kümesinde bir komut dosyası yürütüldüğünde, oluşturduğu bir [conda ortam](https://conda.io/docs/using/envs.html) çalıştırmak komut dosyanızı için. 

Bu dosyada, komut dosyası yürütme için gereken Python paketlerini belirtin. Azure ML deneme Hizmet bağımlılıkları listesi göre Docker görüntüsündeki conda ortamı oluşturur. Paketlerin listesini burada yürütme altyapısı tarafından erişilebilir olması gerekir. Bu nedenle, paketleri kanallarında gibi listelenmiş olması gerekir:

* [continuum.io](https://anaconda.org/conda-forge/repo)
* [Pypı](https://pypi.python.org/pypi)
* Genel olarak erişilebilen bir uç noktası (URL)
* veya bir yerel dosya yolu
* Başkalarının yürütme altyapısı tarafından erişilebilir

>[!NOTE]
>Hdınsight küme üzerinde çalışan Azure ML çalışma ekranı çalıştırma için yalnızca bir conda ortamı oluşturur. Bu, farklı kullanıcıların farklı python ortamları aynı küme üzerinde çalışan olanak tanır.  

Tipik bir örneği burada verilmiştir **conda_dependencies.yml** dosya.
```yaml
name: project_environment
dependencies:
  # Python version
  - python=3.5.2
  
  # some conda packages
  - scikit-learn
  - cryptography
  
  # use pip to install some more packages
  - pip:
     # a package in PyPi
     - azure-storage
     
     # a package hosted in a public URL endpoint
     - https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
     
     # a wheel file available locally on disk (this only works if you are executing against local target)
     - C:\temp\my_private_python_pkg.whl
```

Azure ML çalışma ekranı derlenmeden aynı conda ortamı kullandığı sürece **conda_dependencies.yml** olduğu gibi kalır. Ancak, herhangi bir şey bu dosyada değişirse, Docker görüntüsünün yeniden neden olur.

>[!NOTE]
>Yürütme karşı hedefliyorsanız _yerel_ bağlamı, işlem **conda_dependencies.yml** dosyası **değil** kullanılır. Paket bağımlılıklarını yerel Azure ML çalışma ekranı Python ortamınız için elle yüklenmesi gerekir.

## <a name="sparkdependenciesyml"></a>spark_dependencies.yml
Bir PySpark komut dosyası ve yüklenmesi gereken Spark paketleri gönderdiğinizde bu dosyayı Spark uygulama adını belirtir. Ayrıca, bu Maven depoları bulunabilir Spark paket yanı sıra tüm genel Maven depo da belirtebilirsiniz.

Örnek aşağıda verilmiştir:

```yaml
configuration:
  # Spark application name
  "spark.app.name": "ClassifyingIris"
  
repositories:
  # Maven repository hosted in Azure CDN
  - "https://mmlspark.azureedge.net/maven"
  
  # Maven repository hosted in spark-packages.org
  - "https://spark-packages.org/packages"
  
packages:
  # MMLSpark package hosted in the Azure CDN Maven
  - group: "com.microsoft.ml.spark"
    artifact: "mmlspark_2.11"
    version: "0.5"
    
  # spark-sklearn packaged hosted in the spark-packages.org Maven
  - group: "databricks"
    artifact: "spark-sklearn"
    version: "0.2.0"
```

>[!NOTE]
>Çalışan boyutu gibi ayarlama parametrelerini küme, çekirdeği spark_dependecies.yml dosyasındaki "yapılandırma" bölümüne gidin 

>[!NOTE]
>Python ortamında, komut dosyası yürütme, *spark_dependencies.yml* dosya göz ardı edilir. Spark (ya da Docker veya Hdınsight kümesinde) karşı çalıştırıyorsanız, yalnızca etkisi yoktur.

## <a name="run-configuration"></a>Çalışma yapılandırması
Belirli bir çalıştırma yapılandırmasını belirtmek için dosyaların çifti gereklidir. Bunlar genellikle CLI komutu kullanılarak oluşturulur. Ancak, da olanları çıkma kopyalama, onları yeniden adlandırın ve bunları düzenleyin.

```azurecli
# create a compute target pointing to a VM via SSH
$ az ml computetarget attach remotedocker -n <compute target name> -a <IP address or FQDN of VM> -u <username> -w <password>

# create a compute context pointing to an HDI cluster head-node via SSH
$ az ml computetarget attach cluster -n <compute target name> -a <IP address or FQDN of HDI cluster> -u <username> -w <password> 
```

Bu komut, belirtilen işlem hedefi göre dosyalar çifti oluşturur. İşlem hedef adlı düşünelim _foo_. Bu komut oluşturur _foo.compute_ ve _foo.runconfig_ içinde **aml_config** klasör.

>[!NOTE]
> _yerel_ veya _docker_ çalıştırma yapılandırma dosyalarını rasgele için adları. Azure ML çalışma ekranı size kolaylık olması için boş bir proje oluşturduğunuzda, bu iki yapılandırmaları çalıştırma ekler. Yeniden adlandırabilirsiniz "<run configuration name>.runconfig" proje şablonu ile gelir veya yenilerini istediğiniz herhangi bir ad ile oluşturduğunuz dosyaları.

### <a name="compute-target-namecompute"></a>\<Hedef adı işlem > .compute
_\<Hedef adı işlem > .compute_ dosyasını işlem hedef bağlantı ve yapılandırma bilgilerini belirtir. Ad-değer çifti listesidir. Aşağıdaki desteklenen ayarları şunlardır.

**tür**: işlem ortam türü. Desteklenen değerler şunlardır:
  - Yerel
  - Docker
  - remotedocker
  - küme

**baseDockerImage**: Python/PySpark komut dosyasını çalıştırmak için kullanılan Docker görüntüsü. Varsayılan değer _microsoft/mmlspark:plus-0.7.91_. Ayrıca başka bir görüntü destekliyoruz: _microsoft/mmlspark:plus-gpu-0.7.91_, hangi size GPU erişim için ana bilgisayar makinesi (GPU mevcut değilse).

**Adres**: IP adresi veya FQDN (tam etki alanı adı) sanal makinenin veya Hdınsight küme baş düğümü.

**Kullanıcı adı**: sanal makine ya da Hdınsight baş düğüm erişmek için SSH kullanıcı adı.

**Parola**: SSH bağlantısı için şifrelenmiş parola.

**sharedVolumes**: Bu yürütme altyapısı, Docker kullanması gereken sinyal bayrağı paylaşılan proje dosyalarını geri ve İleri sevk etmek için Toplu özellik. Docker projeleri kopyalamak zorunda kalmadan doğrudan erişmek için bu yana açık olduğunda bu bayrak sahip yürütmesini kurma hızlandırabilir. Ayarlamak en iyisidir _false_ Docker Windows anormal için birimi paylaşan itibaren Docker altyapısına Windows üzerinde çalışıp çalışmadığını. Ayarlamak _true_ macOS ya da Linux üzerinde çalışıyorsa.

**nvidiaDocker**: ayarlandığında bu bayrak, _true_, kullanılacak Azure ML deneme hizmeti söyler _NVIDIA docker_ komutu normal aksine _docker_ Docker görüntü başlatmak için komutu. _NVIDIA docker_ altyapısı erişim GPU donanım için Docker kapsayıcısı sağlar. GPU yürütme Docker kapsayıcısı içinde çalıştırmak istiyorsanız gerekli bir ayardır. Yalnızca Linux ana destekleyen _NVIDIA docker_. Örneğin, Linux tabanlı DSVM Azure ile birlikte _NVIDIA docker_. _NVIDIA docker_ şimdi itibariyle Windows üzerinde desteklenmiyor.

**nativeSharedDirectory**: Bu özellik, temel dizin belirtir (örneğin: _~/.azureml/share/_) dosyaları arasında paylaşılması için kaydedilebileceği aynı işlem hedef çalıştırır. Bu ayar bir Docker kapsayıcısı üzerinde çalışırken kullandıysanız _sharedVolumes_ ayarlanmalıdır true. Aksi takdirde yürütme başarısız olur.

### <a name="run-configuration-namerunconfig"></a>\<Yapılandırma adı Çalıştır > .runconfig
_\<Yapılandırma adı Çalıştır > .runconfig_ Azure ML denemeler yürütme davranışını belirtir. Ne yanı sıra diğer birçok kullanmak için hedef işlem veya izleme çalıştırma geçmişi gibi yürütme davranışları yapılandırabilirsiniz. Çalışma yapılandırması dosyaların adlarını Azure ML çalışma ekranı masaüstü uygulaması yürütme bağlamı açılır doldurmak için kullanılır.

**ArgumentVector**: Bu bölümde bu yürütme ve komut dosyası için parametreleri parçası olarak çalıştırmak için komut dosyasını belirtir. Örneğin, aşağıdaki kod parçacığında varsa, "<run configuration name>.runconfig" dosyası 

```
 "ArgumentVector":[
  - "myscript.py"
  - 234
  - "-v" 
 ] 
```
_"az ml deneme gönderme foo.runconfig"_ komutuyla otomatik olarak çalışır _myscript.py_ 234 bir parametre ve kümeleri geçirme dosya ayrıntılı bayrağı.

**Hedef**: Bu parametre adıdır _.compute_ dosya _runconfig_ dosya başvuruları. Genellikle işaret _foo.compute_ dosyası, ancak düzenleyebilir, farklı işlem hedefe işaret edecek şekilde.

**Ortam değişkenleri**: Bu bölümde, ortam değişkenleri, çalışmalarına bir parçası olarak ayarlamak kullanıcıların sağlar. Kullanıcı şu biçimde ad-değer çiftleri kullanarak ortam değişkenleri belirtebilirsiniz:
```
EnvironmentVariables:
"EXAMPLE_ENV_VAR1": "Example Value1"
"EXAMPLE_ENV_VAR2": "Example Value2"
```

Bu ortam değişkenleri kullanıcının kodda erişilebilir. Örneğin, "EXAMPLE_ENV_VAR" adlı ortam değişkeni bu phyton kodu yazdırır
```
print(os.environ.get("EXAMPLE_ENV_VAR1"))
```

**Framework**: Bu özellik, Azure ML çalışma ekranı komut dosyasını çalıştırmak için bir Spark oturum başlatma belirtir. Varsayılan değer _PySpark_. Ayarlamak _Python_ iş yükü daha azdır ile daha hızlı başlatma yardımcı olabilecek PySpark kod çalıştırmıyorsanız.

**CondaDependenciesFile**: Bu özellik conda ortamı bağımlılıkları belirtir dosyasını işaret *aml_config* klasör. Varsa kümesine _null_, varsayılan işaret **conda_dependencies.yml** dosya.

**SparkDependenciesFile**: Bu özellik Spark bağımlılıkları belirtir dosyasını işaret **aml_config** klasör. Ayarlanır _null_ varsayılan ve bu işaret varsayılan **spark_dependencies.yml** dosya.

**PrepareEnvironment**: ayarlandığında bu özellik, _doğru_, ilk çalıştırma bir parçası olarak belirtilen conda bağımlılıkları göre conda ortamını hazırlamak için deneme hizmet söyler. Bu özellik, yalnızca bir Docker ortamında yürüttüğünüzde etkilidir. Karşı çalıştırıyorsanız, bu ayar etkisizdir bir _yerel_ ortamı. 

**TrackedRun**: Bu bayrağı deneme hizmeti Azure ML geçmişi altyapısında çalışma ekranı Çalıştır izlemek gerekip gerekmediğini işaret eder. Varsayılan değer _doğru_. 

**UseSampling**: _UseSampling_ veri kaynakları için etkin örnek veri kümesi çalıştırmak için kullanılıp kullanılmayacağını belirtir. Varsa kümesine _yanlış_, veri kaynaklarını alma ve veri deposundan okuma tam veri kullanın. Varsa kümesine _doğru_, etkin örnekleri kullanılır. Kullanıcılar ** DataSourceSettings "etkin örnek devre dışı bırakmak isterseniz kullanmak için hangi belirli örnek veri kümesi belirtmek için. 

**DataSourceSettings**: Bu yapılandırma bölümü veri kaynağı ayarlarını belirtir. Bu bölümde, kullanıcı belirli bir veri kaynağı için mevcut hangi veri örneği Çalıştır bir parçası olarak kullanıldığını belirtir. 

Şu yapılandırma ayarı "MySample" adlı bu örnek "gelen veriKaynağım ' a" adlı veri kaynağı için kullanıldığını belirtir
```
DataSourceSettings:
    MyDataSource.dsource:
    Sampling:
    Sample: MySample
```

**DataSourceSubstitutions**: kullanıcı bir veri kaynağından kendi kodunu değiştirmeden diğerine geçmek istediğinde, veri kaynağı değişimler kullanılabilir. Örneğin, kullanıcıların Azure Blob veri kaynağı başvurusu değiştirerek depolanan özgün, büyük veri kümesi için bir örneklenen aşağı, yerel dosyadan geçiş yapabilirsiniz. Bir değiştirme kullanıldığında, Azure ML çalışma ekranı veri kaynakları ve veri hazırlık paketleri, alternatif veri kaynağı başvurarak çalışır.

Aşağıdaki örnek Azure ML veri kaynakları ve veri hazırlık paketleri "mylocal.datasource" başvurularında "myremote.dsource" ile değiştirir. 
 
```
DataSourceSubstitutions:
    myocal.dsource: myremote.dsource
```

Yukarıdaki değiştirme bağlı olarak, aşağıdaki kod örneği şimdi "myremote.dsource" "mylocal.dsource" yerine kendi kodunu değiştirme kullanıcılar okur.
```
df = datasource.load_datasource('mylocal.dsource')
```
## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [Deneme hizmet yapılandırmasını](experimentation-service-configuration.md).
