

Azure için web uygulaması projesi oluşturduğunuzda, azure'da sanal makine sağlayabilirsiniz. Ek yazılım ile Merhaba sanal makine yapılandırma veya hello sanal makine hata ayıklama veya tanılama amaçları için kullanın.

toocreate bir web uygulaması oluşturduğunuzda, bir sanal makineye aşağıdaki adımları izleyin:

1. Visual Studio'da sırasıyla **dosya** > **yeni** > **proje** > **Web**ve ardından seçin **ASP.NET Web uygulaması** (Merhaba altında **Visual C#** veya **Visual Basic** düğümler).
2. Merhaba, **yeni ASP.NET projesi** iletişim kutusu, select hello türü ve hello Azure hello iletişim kutusunda (Merhaba sağ alt köşedeki) bölümünde, o hello emin olun, web uygulamasının **hellobuluttakikonağa**onay kutusu seçilidir (Bu onay kutusunu etiketli **uzak kaynaklar Oluştur** bazı yüklemeler içinde).
   
    ![][0]
3. Bu örneğin Microsoft Azure altında hello aşağı açılan listesinde seçin **sanal makine (v1)**ve ardından hello **Tamam** düğmesi.
4. İstenirse tooAzure oturum açın. Merhaba **sanal makine oluşturma** iletişim kutusu görüntülenir.
   
    ![][2]
5. Merhaba, **DNS adı** kutusuna, hello sanal makine için bir ad girin. Merhaba DNS adının Azure'da benzersiz olması gerekir. Girdiğiniz hello adı yoksa, kırmızı bir ünlem işareti görüntülenir.
6. Merhaba, **görüntü** listesinde, toobase hello sanal makine üzerinde hello görüntü seçin. Merhaba standart Azure sanal makine görüntülerini veya görüntünüzü tooAzure yüklediğiniz herhangi birini seçebilirsiniz.
7. Merhaba bırakın **IIS etkinleştirmek ve Web dağıtımı** tooinstall farklı bir web sunucusuna planlamıyorsanız onay kutusu. Web dağıtımı devre dışı bırakırsanız Visual Studio'dan mümkün toopublish olmayacaktır. Paketlenmiş hello Windows Server görüntülerinin, kendi özel görüntülerinizi de dahil olmak üzere, IIS ve Web dağıtımı tooany ekleyebilirsiniz.
8. Merhaba, **boyutu** listesinde, hello hello sanal makine boyutunu seçin.
9. Merhaba oturum açma kimlik bilgilerini bu sanal makine belirtin. Bunları Not, bunları gerekir çünkü tooaccess makinesine Uzak Masaüstü aracılığıyla hello.
10. Merhaba, **konumu** listesinde, hello bölge toohost hello sanal makineyi seçin.
11. Merhaba tıklatın **Tamam** düğmesini toostart hello sanal makine oluşturma. Merhaba hello işlemde hello ilerlemesini izleyebilirsiniz **çıkış** penceresi.
    
    ![][3]
12. Merhaba sanal makine sağladığında, yayımlanan betikleri oluşturulan bir **PublishScripts** çözümünüzdeki düğümü. Merhaba komut çalıştırır ve hükümleri Azure'da bir sanal makine yayımladı. Merhaba **çıkış** penceresinde hello durumu gösterilir. Merhaba betik eylemleri tooset hello sanal makineyi aşağıdaki hello gerçekleştirir:
    
    * Zaten yoksa hello sanal makine oluşturur.
    * İle başlayan bir ada sahip bir depolama hesabı oluşturur `devtest`, ancak yalnızca hiç zaten varsa bu tür bir depolama hesabı hello belirtilen bölgede.
    * Merhaba sanal makine için bir kapsayıcı olarak bir bulut hizmeti oluşturur ve Merhaba web uygulaması için bir web rolü oluşturur.
    * Web dağıtımı hello sanal makinede yapılandırır.
    * IIS ve ASP.NET hello sanal makinede yapılandırır.
    
    ![][4]
13. (İsteğe bağlı) Toohello yeni sanal makineye bağlanabilir. İçinde **Sunucu Gezgini**, hello genişletin **sanal makineleri** düğümü, oluşturduğunuz hello sanal makine için ve kısayol menüsünde hello düğümü seçin, seçin **Uzak Masaüstü'nüileBağlan**. Alternatif olarak, içinde **Cloud Explorer** seçebileceğiniz **portalında açık** hello kısayol menüsünü ve toohello sanal makineye bağlanmak.
    
    ![][5]

## <a name="next-steps"></a>Sonraki adımlar
Okuma sırasında daha ayrıntılı bilgi istiyorsanız toocustomize hello yayımlanan komut dosyaları, oluşturduğunuz [Windows PowerShell komut dosyalarını kullanarak tooPublish tooDev ve Test ortamları](http://msdn.microsoft.com/library/dn642480.aspx).

[0]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_NewProject.PNG
[1]: ./media/dotnet-visual-studio-create-virtual-machine/CreateVM_SignIn.PNG
[2]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_CreateVM.PNG
[3]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_Provisioning.png
[4]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_SolutionExplorer.png
[5]: ./media/virtual-machines-common-classic-web-app-visual-studio/VS_Create_VM_Connect.png
