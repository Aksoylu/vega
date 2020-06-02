# Untitled

**Vega Kütüphanesi**

**Vega Hakkında :**

* Vega, basit derin öğrenme amacı ile Ümit Aksoylu tarafından geliştirilen temel prensipte basit bir derin öğrenme kütüphanesidir.
* Şimdilik yalnızca Python ve PHP ile geliştirilmiştir.
* Mevcut sürüm v0.1 ile bir çok eksiklikleri vardır. Bunlar;
  * Henüz Multithreading yapısını desteklememektedir. Bu nedenle diğer kütüphanelere kıyasla fazla yavaş çalışabilir.
  * GPU tarafından henüz desteklenmemektedir. Bu da diğer profesyonel kütüphanelere kıyasla öğrenme aşamasında düşük performansa sebep olabilir.
  * Henüz 2’den fazla gizli katman oluşturmayı desteklememektedir.
  * Epoch \(Devir\) kontrol mekanizmalarını henüz desteklememektedir.
  * Henüz tüm aktivasyon fonksiyonlarını ve çok kanallı öğrenme modellerini desteklememektedir.
  * Henüz yalnızca ileri ve geri besleme tabanlı temel öğrenmeyi gerçekleştirebilmektedir. Yinelemeni öğrenme veya genetik algoritma gibi farklı yapay zeka alanlarını henüz barındırmamaktadır.
* Sonuç olarak Vega’nın yalnızca hafif görevler ve kullanım kolaylığına ihtiyaç duyulan durumlarda tercih edilmesi tavsiye edilmektedir.

**Desteklenen Platformlar :**

* Python \(Eğitim ve Çalıştırma\)
* PHP \(Yalnızca Çalıştırma\)

Not: Vega kütüphanesi ile bir modelin oluşturulup bir veri seti ile eğitilmesine kadar olan süreç “Eğitim” olarak adlandırılır. Eğitilmiş ve ağırlıkları optimum hale gelmiş model, öğrenme işleminin ardından JSON formatı ile kütüphane tarafından dosyaya kaydedilir. Bu modelin tekrar belleğe yüklenerek yapay sinir ağının çalıştırılması ise “Çalıştırma” olarak adlandırılmıştır.

**İşlevler**

Yalnızca temel işlevlere sahip olan bu kütüphane ile iki gizli katmana sahip olan bir ağ kolayca oluşturulabilir. Böylece toplamda 4 katmana kadar yapılabilecek tüm makine ve derin öğrenme işlemleri Vega kütüphanesi yardımı ile kolayca yapılabilir.

Vega kütüphanesi, ham veri kullanarak veri sınıflardırma, tahminleme ve üretme işlevlerini yerine getirebilecek bir derin öğrenme kütüphanesidir.

**Vega**, eğitilen bir modelin tüm platformlarda sorunsuzca prediction \(tahmin için çalıştırma\) amacıyla kullanılmasını hedefler.

Örneğin Python ile eğitilmiş bir yapay sinir ağını kaydedip, başka bir platformda hiçbir eklenti kurmaksızın çalıştırabilmeniz için hafiflik ve kolaylık sunması amacıyla geliştirilmiştir.

**Vega Fonksiyonları**

**1- vega.Katman \(Ağ oluşturmak\)**

neuralNetwork = vega.Katman\(\[4,4\], \[36,36\]\)

neuralNetwork isminde ve 2 gizli katmana, toplam 4 katmana sahip, her bir katmanda 4 nöronun ve her nöronun da 36 weight\(bağlantı\) sayısına sahip olduğu bir ağ oluşturur.

İlk parametre olan \[4,4\] 4 nöronlu birinci ve 4 nöronlu ikinci katmanı oluşturur.

İkinci parametre olan \[36,36\] ise birinci katmanda 36, ikinci katmanda da 36 bağlantı \(weight\) oluşturulmasını sağlar.

Örneğin vega.Katman\(\[3,2\], \[12,2\]\) çağrısı, ilk katmanın 3, ikinci katmanın 2 nörona sahip olduğu ve ilk katmandaki nöronların 12 weight sayısı, ikinci katmandaki nöronların ise 2 weight sayısına sahip olduğu bir ağ yapısını inşa eder.

**2- &lt;Ağ&gt;.Name \(Ağ’a isim vermek\)**

neuralNetwork.name = "test\_network"

neuralNetwork adı ile oluşturulan nesne bir yapay sinir ağıdır. Bu ağa .name metodu ile isim verilebilir. Bu verilen isim kullanılarak eğitilmiş ağ Vega tarafından “.neurons” dosyası olarak kaydedilir.

**3- &lt;Ağ&gt;.loadModel \(.neurons dosyasından ağ’ı yüklemek\)**

neuralNetwork.loadModel\("gozs.neurons"\)

**gozs.neurons** dosyasında kayıt edilmiş ağı tekrar belleğe yükler ve kullanıma \(prediction’a\) hazır hale getirir. Eğer katman fonksiyonunu kullanarak bir yapı oluşturmuş iseniz, yüklenilen model ile oluşturduğunuz modelin katman, nöron ve weight sayılarının eşleşmesine özen gösterin. Bu işlemden sonra train fonksiyonunun tekrar çalıştırılmasına ihtiyaç yoktur. Doğrudan feedForward metodu kullanılarak ağ’a tahmin yaptırılabilir.

Not: Eğer ağınızın öğrenmesi yarım kalmış ise ağı yükledikten sonra train fonksiyonunu çalıştırırsanız, ağ kaldığı yerden öğrenmeye devam edecektir.

**4- &lt;Ağ&gt;.train \(Ağı eğitmek\)**

learning\_rate = 0.001

epoch = 1000

\#Now Learning Time

SinirAgi.train\(dataset, targets,learning\_rate, epoch\)

Dataset ve targets nesneleri, aynı sayıda eleman içeren Numpy array nesneleridir. Aynı sayıda nesne içermeleri önemlidir zira dataset’de tahmin edilecek veri ve targets’de de o veri ile eşleşen sonuç içerilmektedir. Yani ağ, dataset verisi ile targets verisi arasında ilişki kuracak biçimde eğitilecektir.

**Learning Rate :** Öğrenme adımıdır. Küçük olması durumunda ağ daha yavaş eğitilebilir. Ancak büyütülürse backPropagation fonksiyonunun yürürlüğe girmeme ihtimali oluşabileceğinden hiç eğitilmeye de bilir. Çoğunlukla deneme yanılma yöntemi ile en iyi learning rate değeri bulunabilir.

**Epoch :** \(aynı\) dataset verisinin ağı eğitmek için kaç defa ağ’dan ileri besleme yolu ile geçirilmesi gerektiği sayısıdır. Yüksek olması öğrenme ihtimalini arttırır ancak aşırı fazla Epoch \(devir\) sayısı, yapay sinir ağının ezberci davranmasını ve dataset-target arası mantıksal ilişki kurmak yerine bu ikişkiyi ezberlemesine sebebiyet verebilir.

**5- &lt;Ağ&gt;.feedforward\(Ağ’da ileri besleme\)**

prediction = neuralNetwork.feedforward\(testData\)

print\(prediction\)

testData nesnesi, ağın eğitilmesi için kullanılan dataset arrayList’inin elemanlarından biri ile aynı yapıda ve eleman sayısında olmalıdır. Ağ, bu veriyi işleyerek buna uygun target layer’ından bir benzetme yapacaktır.

Örneğin ağ eğitilirken sonuçların 1 veya 0 olması ağ’a target verisinde belirtilmişse, eğitilmiş ağ verinizi feedforward metodu ile işledikten size bir değer döndürecektir. Bu değerin 1’e veya 0’a yakın olması \(veya belirlediğiniz aralıkta olması\), işleminiz için anlamlı bir sonuç olacaktır. Böylece eğitilmiş ağ, size istediğiniz biçimde dönüş yapabilir.

**6-&lt;Ağ&gt;.saveLock**

neuralNetwork.saveLock\(True\) \#save model if program closes

True veya False değer alabilir. SaveLock, eğer öğrenme aşamasında program herhangi bir sebepten kapanırsa öğrenmekte olan modelin otomatik olarak kayıt edilmesini sağlar.

**7-&lt;Ağ&gt;.setEpochLock**

neuralNetwork.setEpochLock\(200\) \#save model per 200 epoch

Öğrenme \(Train\) fonksiyonu çalıştırılmadan önce çalıştırılmalıdır. Yukarıdaki örnekte her 200 epoch’da bir yapay sinir ağı modelinin kayıt edilmesini sağlar

**Öğrenme Metodolojisi**

* Epoch ve Learning Rate sayısı en iyi olarak deneme-yanılma yöntemi ile bulunabilir.
* Bir süre sonra Epoch arttıkça düşmesi gereken loss değeri artışa geçebilir. Bu, öğrenmenin tersine \(zararına\) gerçekleştiğini gösterebilir ve olabilecek bir durumdur. Ağ optimum duruma geldiğinde genellikle dropout veya benzeri işlemlerin ağ üzerinde yapılması faydalı olabilir. Vega henüz bu teknikleri içermediğinden el ile yapılması tavsiye edilir.
* Eğer ağ öğreniminin tıkanması durumunda ağırlık değerlerinde rastsal bir filtre uygulanması, geçici bir süre için ağın öğrenimini geri plana atsa da daha ileri gidebilmesi için olanak oluşturabilir.
* Loss değerinin optimum değere geldiğinde öğrenimin kesilmesi gerekir. Öğrenim kesildiğinde ağın kaydedilmesi için saveLock değerinin true olarak ayarlanması önemlidir. Aynı şekilde, kestirebiliyorsanız EpochLock’da sizin için yeterli olacaktır.
* Vega, multithreading desteklemez bu sebeple çok yavaştır. Ancak bu, bilgisayar kaynaklarının çok fazla işgal edilmediği anlamına da gelir. Vega ile öğrenim süreci yavaş olacaktır ancak bilgisayarınızı kullanmanızda bir sorun da hissettirmeyecektir. Vega’nın ileri sürümlerinde bu kullanıcının tercihine sunulmak üzere opsiyonel bir seçenek haline getirilecektir.
* Bir TCP/Soket yordamı ile ağırlıkların birden fazla cihaza gönderilmesi ile paralel öğrenme gerçekleştirilebilir. Bu da dağıtık bir sistem oluşturulması ve bu sistemin bir ağ eğitiminde kullanılmasında işlevsel olabilir. Vega’nın ilerleyen sürümlerinde TCP/Soket yordamı ile dağıtık ağ öğreninin gerçeklenmesi hedeflenmektedir.

\*\*\*\*

