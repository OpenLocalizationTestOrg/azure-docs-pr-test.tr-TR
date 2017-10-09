



Ortamınız ve Seçenekler bağlı olarak, hello betik hello Azure sanal ağı, depolama hesapları, bulut Hizmetleri, etki alanı denetleyicisi, uzak veya yerel SQL veritabanları, baş düğüm ve ek küme de dahil olmak üzere tüm hello küme altyapısı oluşturabilirsiniz düğümleri. Alternatif olarak, hello betik önceden var olan Azure altyapısını kullanır ve yalnızca hello HPC küme düğümleri oluşturun.

HPC Pack küme planlama hakkında arka plan bilgileri için bkz: hello [ürün değerlendirme ve planlama](https://technet.microsoft.com/library/jj899596.aspx) ve [Başlarken](https://technet.microsoft.com/library/jj899590.aspx) hello HPC Pack 2012 R2 TechNet Kitaplığı'nda içeriği.

## <a name="prerequisites"></a>Ön koşullar
* **Azure aboneliği**: her iki hello Azure genel ya da Azure Çin hizmeti bir aboneliği kullanabilirsiniz. Abonelik sınırlarınızı hello sayısı ve türü dağıtabilmeniz için küme düğümlerinin etkiler. Bilgi için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../articles/azure-subscription-service-limits.md).
* **Azure PowerShell 0.8.10 ile Windows istemci bilgisayarı veya sonrası yüklü ve yapılandırılmış**: bkz [Azure PowerShell ile çalışmaya başlama](/powershell/azureps-cmdlets-docs) yükleme yönergeleri ve adımları tooconnect tooyour Azure aboneliği için.
* **HPC Pack Iaas dağıtım betiği**: karşıdan yükle ve en son sürümünü hello hello betikten hello paket [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Merhaba betik Hello sürümünü çalıştırarak denetleme `New-HPCIaaSCluster.ps1 –Version`. Bu makalede hello betik sürüm 4.5.2 temel alır.
* **Yapılandırma betiği**: hello betik tooconfigure hello HPC Kümesi kullanan bir XML dosyası oluşturun. Bilgi ve örnekler için bu makalenin sonraki bölümlerinde bölümlere bakın ve dosya hello dağıtım betiği eşlik Manual.rtf hello.

## <a name="syntax"></a>Sözdizimi
```PowerShell
New-HPCIaaSCluster.ps1 [-ConfigFile] <String> [-AdminUserName]<String> [[-AdminPassword] <String>] [[-HPCImageName] <String>] [[-LogFile] <String>] [-Force] [-NoCleanOnFailure] [-PSSessionSkipCACheck] [<CommonParameters>]
```
> [!NOTE]
> Merhaba komut dosyasını bir yönetici olarak çalıştırın.
> 
> 

### <a name="parameters"></a>Parametreler
* **ConfigFile**: hello yapılandırma dosyası toodescribe hello HPC küme hello dosya yolunu belirtir. Merhaba yapılandırma dosyası bu konudaki veya Manual.rtf hello komut dosyasını içeren hello klasöründeki hello dosyasında hakkında daha fazla bakın.
* **AdminUserName**: hello kullanıcı adını belirtir. Merhaba etki alanı ormanı hello komut dosyası tarafından oluşturduysanız, bu tüm VM'ler için hello yerel yönetici kullanıcı adı ve hello etki alanı yöneticisi adı olur. Merhaba etki alanı ormanı zaten varsa, yerel yönetici kullanıcı adı tooinstall HPC Pack Merhaba gibi bu hello etki alanı kullanıcısı belirtir.
* **Admınpassword**: Merhaba yönetici parolasını belirtir. Merhaba komut satırında belirtilmezse, hello betik tooinput hello parola ister.
* **HPCImageName** (isteğe bağlı): hello HPC Pack VM görüntü adı kullanılan toodeploy hello HPC Kümesi belirtir. Hello Azure Marketi sağlanan Microsoft HPC Pack görüntüden olmalıdır. Belirtilmemiş (önerilen genellikle), Merhaba, komut dosyası seçtiği son yayımlanan hello [HPC Pack 2012 R2 görüntüsünü](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/). Windows Server 2012 R2 Datacenter HPC Pack 2012 R2 güncelleştirme 3 ile Merhaba son görüntü dayanır.
  
  > [!NOTE]
  > Geçerli bir HPC Pack görüntüsü belirtmezseniz dağıtımı başarısız olur.
  > 
  > 
* **Günlük dosyası** (isteğe bağlı): hello dağıtım günlük dosyası yolunu belirtir. Belirtilmezse, hello betik hello temp dizininde hello betik çalıştıran hello bilgisayarın bir günlük dosyası oluşturur.
* **Zorla** (isteğe bağlı): tüm hello onay komut istemlerini bastırır.
* **NoCleanOnFailure** (isteğe bağlı): Bu hello değil başarıyla dağıtılan Azure VM'ler kaldırılmaz belirtir. Merhaba betik toocontinue hello dağıtımı yeniden çalıştırmadan önce bu Vm'lere el ile kaldırın veya başlangıç dağıtımı başarısız olabilir.
* **PSSessionSkipCACheck** (isteğe bağlı): Bu komut dosyası tarafından dağıtılan VM'ler ile her bulut hizmeti için otomatik olarak imzalanan bir sertifika Azure tarafından otomatik olarak oluşturulur ve hello bulut hizmetindeki tüm hello VM'ler, varsayılan Windows hello gibi bu sertifikayı kullanın Uzaktan Yönetim (WinRM) sertifikası. toodeploy HPC özellikleri bu Azure VM'de hello betik varsayılan geçici olarak yükler. Bu sertifikaların hello yerel bilgisayar\\hello istemci bilgisayar toosuppress güvenilen kök sertifika yetkilileri deposunda hello "CA güvenilir değil" güvenlik betik yürütme sırasında hata oluştu. Merhaba betik tamamlandığında hello sertifikaları kaldırılır. Bu parametre belirtilmezse, hello sertifikaları hello istemci bilgisayarda yüklü değil ve hello güvenlik uyarısı engellenir.
  
  > [!IMPORTANT]
  > Bu parametre, üretim dağıtımları için önerilmez.
  > 
  > 

### <a name="example"></a>Örnek
Merhaba aşağıdaki örnek yapılandırma dosyası kullanarak bir HPC Pack kümesini oluşturur *MyConfigFile.xml*ve hello Küme yükleme için yönetici kimlik bilgilerini belirtir.

```PowerShell
.\New-HPCIaaSCluster.ps1 –ConfigFile MyConfigFile.xml -AdminUserName <username> –AdminPassword <password>
```

### <a name="additional-considerations"></a>Diğer konular
* Merhaba betik isteğe bağlı olarak hello HPC paketi web portalı veya hello HPC Pack REST API aracılığıyla iş gönderme etkinleştirebilirsiniz.
* tooinstall ek yazılım veya diğer ayarları yapılandırmak istiyorsanız hello betik isteğe bağlı olarak özel öncesi ve sonrası yapılandırma hello baş düğümünde çalıştırabilir.

## <a name="configuration-file"></a>Yapılandırma dosyası
Merhaba yapılandırma dosyası hello dağıtım komut dosyası için bir XML dosyasıdır. Merhaba şema dosyası HPCIaaSClusterConfig.xsd hello HPC Pack Iaas dağıtım komut dosyası klasöründe bulunur. **IaaSClusterConfig** Manual.rtf hello dağıtım komut dosyası klasöründeki hello dosyasında ayrıntılı açıklanan hello alt öğeleri içerir hello yapılandırma dosyasının kök öğesinin hello olduğu.

