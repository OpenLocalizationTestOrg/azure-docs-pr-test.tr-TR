

## <a name="deployment-considerations"></a>Dağıtma konuları
* **Azure aboneliği** – birkaç işlem yoğunluklu örnekler, birden çok toodeploy Kullandıkça Öde aboneliğine veya diğer satın alma seçenekleri dikkate alın. [Ücretsiz Azure hesabı](https://azure.microsoft.com/free/) kullanıyorsanız, yalnızca sınırlı sayıda Azure işlem çekirdeği kullanabilirsiniz.

* **Fiyatlandırma ve kullanılabilirlik** -bu VM boyutları yalnızca hello standart fiyatlandırma katmanında sunulur. [Ürünler kullanılabilir bölgeye göre] denetleyin (https://azure.microsoft.com/regions/services/) Azure bölgelerindeki kullanılabilirlik. 
* **Çekirdek kota** – Azure aboneliğinizde hello varsayılan değerinden tooincrease hello çekirdek kota gerekebilir. Aboneliğinizi de hello hello H-serisi dahil olmak üzere belirli VM boyutu aileleri, dağıtabilirsiniz çekirdek sayısını sınırlayabilir. toorequest kota artırma, [bir çevrimiçi müşteri destek isteği açma](../articles/azure-supportability/how-to-create-azure-support-request.md) herhangi bir ücret alınmaz. (Varsayılan sınırları abonelik kategoriye göre farklılık gösterebilir.)
  
  > [!NOTE]
  > Büyük ölçekli kapasite gereksinimlerini varsa Azure desteğine başvurun. Azure kotaları alacak olan sınırlar, değil kapasite garantiler. Kotanızı bağımsız olarak, kullandığınız yalnızca çekirdek için ücretlendirilirsiniz.
  > 
  > 
* **Sanal ağ** – Azure bir [sanal ağ](https://azure.microsoft.com/documentation/services/virtual-network/) gerekli değil toouse hello işlem yoğunluklu örnekler geçerlidir. Ancak, birçok dağıtımları için en az bir bulut tabanlı Azure sanal ağı gerekir veya tooaccess gerekiyorsa bir siteden siteye bağlantı şirket içi kaynaklar. Gerekli olduğunda, yeni bir sanal ağ toodeploy hello örneği oluşturun. Bir benzeşim grubunda işlem yoğunluklu VM'ler tooa sanal ağ ekleme desteklenmiyor.
* **Yeniden boyutlandırma** – kendi özelleştirilmiş donanım nedeniyle işlem yoğunluklu örnekler yalnızca boyutlandırabilirsiniz hello içinde aynı aile (S-serisi veya işlem yoğunluklu A-series) boyut. Örneğin, yalnızca bir H-serisi boyutu tooanother H-serisi VM'den boyutlandırabilirsiniz. Buna ek olarak, yoğun olmayan boyutu tooa işlem yoğunluklu sabit boyutlu bir yeniden boyutlandırma desteklenmiyor.  
