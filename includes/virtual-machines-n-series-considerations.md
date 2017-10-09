## <a name="deployment-considerations"></a>Dağıtma konuları

* N-serisi VM'ler kullanılabilirlik için bkz: [bölgeye göre ürünleri](https://azure.microsoft.com/en-us/regions/services/).

* N-serisi VM'ler yalnızca hello Resource Manager dağıtım modelinde dağıtılabilir.

* Ne zaman kullanarak bir N-serisi VM oluşturma izin ver hello Azure Portal'da, hello **Temelleri** dikey penceresinde, select bir **VM disk türü** , **HDD**. Merhaba üzerinde toochoose kullanılabilir N-serisi bir boyut **boyutu** dikey penceresinde tıklatın **tüm görüntüle**.

* N-serisi VM'ler Azure Premium storage tarafından yedeklenen VM diskleri desteklemez.

* Birden fazla birkaç N-serisi VM'ler toodeploy istiyorsanız, Kullandıkça Öde aboneliğine veya diğer satın alma seçenekleri göz önünde bulundurun. [Ücretsiz Azure hesabı](https://azure.microsoft.com/free/) kullanıyorsanız, yalnızca sınırlı sayıda Azure işlem çekirdeği kullanabilirsiniz.

* Azure aboneliğinizde tooincrease hello çekirdek kota (her bölge) gerekir ve NC veya NV çekirdekleri hello ayrı Kotayı artırmak. toorequest kota artırma, [bir çevrimiçi müşteri destek isteği açma](../articles/azure-supportability/how-to-create-azure-support-request.md) herhangi bir ücret alınmaz. Varsayılan sınır abonelik kategoriye göre farklılık gösterebilir.

* N-serisi sanal makineler dağıtabileceğiniz bir VM görüntüsü olan hello [Azure veri bilimi sanal makine](../articles/machine-learning/machine-learning-data-science-virtual-machine-overview.md). Merhaba veri bilimi sanal makine, önceden yükleyen ve birçok popüler veri bilimi ve araçları öğrenme derin yapılandırır. NC örnekleri için NVIDIA Tesla GPU sürücülerinin çalışmasını engeller.





