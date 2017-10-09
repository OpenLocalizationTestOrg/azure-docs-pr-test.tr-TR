Tooa bağlanan her istemci bilgisayar noktadan siteye kullanarak VNet yüklü bir istemci sertifikası olması gerekir. Merhaba istemci sertifikası hello kök sertifikasından oluşturulur ve her istemci bilgisayarda yüklü. Geçerli bir istemci sertifikası yüklü değil ve tooconnect toohello VNet hello istemci çalışırsa, kimlik doğrulaması başarısız olur.

Her istemci için ya da benzersiz bir sertifika oluşturabilir veya birden çok istemci için aynı sertifika hello kullanabilirsiniz. Merhaba avantajı toogenerating benzersiz istemci sertifikaları hello özelliği toorevoke tek bir sertifika var. Aksi takdirde, birden çok istemci aynı istemci sertifikası hello kullanarak ve toorevoke gerekir, toogenerate olması ve tüm bu sertifika tooauthenticate kullanan istemciler hello yeni sertifika yükleyin.

Yöntemler aşağıdaki hello kullanarak istemci sertifikalarını oluşturabilir:

- **Kurumsal sertifika:**

  - Kurumsal bir sertifika çözümü kullanıyorsanız, bir istemci sertifikası hello ortak adı değeri biçimi ile Oluştur 'name@yourdomain.com', hello 'etki alanı adı\kullanıcı adı' biçimi yerine.
  - Merhaba istemci sertifikası 'İstemci kimlik doğrulaması' hello kullan listesindeki ilk öğeyi hello sahip hello 'User' sertifika şablonuna dayalı emin olmak yerine akıllı kart oturum açma, vb.. Merhaba istemci sertifikası çift ve görüntüleme hello sertifika denetleyebilirsiniz **ayrıntıları > Gelişmiş anahtar kullanımı**.

- **Otomatik olarak imzalanan sertifika:** hello P2S sertifika makaleleri aşağıdaki hello adımlarını izleyin önemlidir. Aksi takdirde, oluşturduğunuz hello istemci sertifikalarını P2S bağlantılarının ile uyumlu olmayacak ve istemcileri tooconnect çalışırken bir hata alır. makaleler hello birini Hello adımlarda uyumlu istemci sertifikası oluşturma: 

  * [Windows 10 PowerShell yönergeleri](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientcert): Bu yönergeleri Windows 10 ve PowerShell toogenerate sertifikaları gerektirir. oluşturulan hello sertifikalarını tüm desteklenen P2S istemcide yüklenebilir.
  * [MakeCert yönergeleri](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md): erişim tooa Windows 10 bilgisayar toouse toogenerate sertifikaları yoksa MakeCert kullanın. MakeCert kullanım ancak MakeCert toogenerate sertifikaları kullanmaya devam edebilirsiniz. oluşturulan hello sertifikalarını tüm desteklenen P2S istemcide yüklenebilir.

  Yönergeler önceki hello kullanarak otomatik olarak imzalanan kök sertifikasından bir istemci sertifikası oluşturduğunuzda, otomatik olarak toogenerate kullanılan hello bilgisayarda yüklü. Tooinstall başka bir istemci bilgisayarında bir istemci sertifikası istiyorsanız tooexport gerekir hello tüm sertifika zincirini birlikte bir .pfx olarak. Merhaba istemci toosuccessfully kimlik doğrulaması için gerekli olan hello kök sertifika bilgilerini içeren bir .pfx dosyası oluşturur. Adımları tooexport bir sertifika için bkz: [sertifikalar - bir istemci sertifikası verme](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientexport).
