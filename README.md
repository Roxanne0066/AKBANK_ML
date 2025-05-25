# AKBANK - Global AI Hub_ML

Bu repo AKBANK - Global AI Hub Machine Learning BootCamp preojesi için hazırlanmıştır.

# Giriş

## Projenin Amacı ve Çözdüğü Problem
Bu projemde amaç, MR sonucu alınan görüntülerin Daha hızlı işlenmesi, belki doktorların göremediği veya dikkatinden kaçması sonucu oluşan sorunları önlemek, daha gelişmiş bir algoritma ile tümörün erken teşhisini sağlayıp kayıpları olabildiğince azaltmaktır.

## Veri Seti
*Kaynak : https://www.kaggle.com/datasets/navoneel/brain-mri-images-for-brain-tumor-detection
*Boyut : 16MB
*İçerik Yaklaşık 253 resim ve 2 Label bulunmaktadır (yes , No)

# METRİKLER

## Veri Hazırlığı ve Artırma (Data Preprocessing and Augmentation)

Bu projede, beyin MR'ı görüntülerinden oluşan veri seti, CNN modelimizin eğitimi için dikkatli bir ön işleme ve veri artırma sürecinden geçirilmiştir:

### Yeniden Boyutlandırma ve Normalizasyon:
Modelin tutarlı bir şekilde çalışabilmesi için tüm görüntüler standart bir boyuta getirilmiş ve piksel değerleri, modelin daha verimli öğrenmesini sağlamak amacıyla 0-1 aralığına normalize edilmiştir.

### Veri Artırma (Data Augmentation):
Modelin daha iyi öğrenip daha stabil çalışması ve aşırı öğrenmenin önüne geçmek için için bazı teknikler uygulanmıştır. Bu teknikler arasında görüntülerin rastgele;

Döndürülmesi (rotation_range)

Yatay ve dikey olarak kaydırılması (width_shift_range, height_shift_range)

Makaslama (eğme) işlemine tabi tutulması (shear_range)

Yakınlaştırılıp uzaklaştırılması (zoom_range)

Ve yatay eksende çevrilmesi (horizontal_flip) bulunmaktadır.

Bu sayede, modelimiz her eğitim turunda aynı resimlerin farklı varyasyonlarını görerek daha zengin ve çeşitli bir veri üzerinde eğitilmiştir.

### Veri Setinin Bölünmesi: 

Modelin eğitimi ve performansının tarafsız bir şekilde değerlendirilebilmesi için veri seti, %80 eğitim ve %20 doğrulama (validation) olmak üzere iki alt kümeye ayrılmıştır.

### Model Mimarisi (Evrişimli Sinir Ağı - CNN)

Model olarak CNN tercih edilmesi, görüntü sınıflandırmada kanıtlanmış yüksek başarısından kaynaklanmaktadır. Model Keras kütüphanesi kullanarak katmanlı bir yapıda oluşturulmuştur. Temel amacı, görüntülerdeki hiyerarşik özellikleri (kenarlar, dokular, şekiller gibi) öğrenerek anlamlı bir sınıflandırma yapmaktır.

### Genel Performans:

Modelimiz, doğrulama seti üzerinde %82.00 genel doğruluk (accuracy) oranına ulaşmıştır. Bu, modelin yaptığı tahminlerin %82'sinin doğru olduğu anlamına gelir. Doğrulama kaybı (loss) ise 0.4752 olarak ölçülmüştür, bu da modelin tahminlerinin gerçek değerlerden ortalama sapmasını gösterir.

### Yorumlar ve Çıkarımlar :

Elde edilen %82'lik doğruluk oranı, projenin veri setinin küçüklüğü düşünüldüğünde iyi bir sonuç verdiği söylenebilir. Model özellikle tümörlü fotoğrafların tespitinde oldukça başarılıdır.  Tümörlü resimlerin tespitinde 5 Yanlış Negatif vermesi( TN ), potansiyelinin yüksek olduğunu göstermektedir.

Sonuç olarak, geliştirilen CNN modeli, beyin tümörü tespitinde temel bir başarı göstermiş olup, metrikler modelin güçlü ve zayıf yönleri hakkında önemli bilgiler sunmaktadır. Gelecek çalışmalarda, özellikle Yanlış Negatif ve Yanlış Pozitif sayılarının azaltılmasına yönelik iyileştirmeler hedeflenebilir.

# Sonuç ve Gelecek Çalışmalar

### Sonuç
Bu proje kapsamında, Akbank Makine Öğrenmesi Bootcamp'i için, Gözetimli Öğrenme teknikleri kullanılarak beyin MR görüntülerinden tümör varlığını tespit eden bir Evrişimli Sinir Ağı (CNN) modeli başarıyla geliştirilmiş ve değerlendirilmiştir.

Kullanılan veri seti üzerinde yapılan dikkatli ön işleme, etkili veri artırma (data augmentation) stratejileri ve ReduceLROnPlateau gibi geri çağırımlar (callbacks) ile optimize edilen eğitim süreci sonucunda, modelimiz doğrulama (validation) seti üzerinde %82 genel doğruluk (accuracy) oranına ulaşmıştır.

Karışıklık matrisi ve sınıflandırma raporu gibi detaylı metrikler incelendiğinde, modelin özellikle tümörlü ("yes") vakaları %84 duyarlılık (recall) ve %87 kesinlik (precision) ile tespit etme başarısı gösterdiği, tümörsüz ("no") vakalarda ise %79 duyarlılık ve %75 kesinlik elde ettiği görülmüştür.

Bu sonuçlar, derin öğrenme modellerinin tıbbi görüntü analizi alanında, özellikle tümör tespiti gibi kritik görevlerde umut verici bir potansiyele sahip olduğunu göstermektedir. Proje, veri analizi, model geliştirme ve değerlendirme konularında pratik deneyim kazandırmıştır.

### Gelecek Çalışmalar 

  ### Veri Setinin Genişletilmesi ve Çeşitlendirilmesi:

  Küçük veri seti daha az doğruluk oranı verdiğini biliyoruz. Bu durumda veri setini arttırmak doğruluğu büyük oranda arttıracaktır.
  İleride başka hastanelerden farklı görseller ile zenginleştirilmesiyle beraber daha iyi sonuçlar elde edilebilir.

  ### Gözetimsiz Öğrenme ile Entegrasyon: 
  Aynı veri seti üzerinde kümeleme gibi gözetimsiz öğrenme uygulamalarıyla gözetimsiz öğrenme üzerine de bilgilerimizi geliştirip     uygulamaya dökebiliriz.

  ### Modelin Deploy Edilmesi (Web Arayüzü ): 
  Eğitilen modelin Streamlit gibi araçlar kullanarak bir başkasına ihtiyaç kalmadan interaktif olarak veriyi verip sonucunun ne olduğu veri sahibi tarafından öğrenilebilir bunun sonucunda da daha hızlı aksiyona geçilebilir.



Bu proje, yapay zeka ve makine öğrenmesi alanındaki temel becerileri pekiştirmekle kalmamış, aynı zamanda bu teknolojilerin sağlık sektöründeki dönüştürücü potansiyelini de gözler önüne sermiştir. Öğrenilen teknikler ve elde edilen deneyim, gelecekteki daha karmaşık problemlere uygulanabilir bir zemin hazırlamıştır.




# LİNKLER

## Dataset link : https://www.kaggle.com/datasets/navoneel/brain-mri-images-for-brain-tumor-detection
Kaggle çalışma ortamı : https://www.kaggle.com/code/emredem1rr/akbank-ml-bootcamp















