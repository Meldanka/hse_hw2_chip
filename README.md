# hse_hw2_chip
google colab: https://colab.research.google.com/drive/12n6AN--Z8ToVHmSEp-6T5zl3gUSvtdmA?usp=sharing
* C помощью анализа ChIP-Seq данных определим участки, где есть конкретная гистоновая модификация в заданном типе клеток.
*  Я взяла клеточную линию H9 и гистоновую метку H4K8ac.

**Отчеты Fastqc:**
*  1) Для ENCFF974MOD все харатеристики оказались в норме, все зеленые галочки кроме двух оранжевых восклицательных знаков Per sequence GC content и Overrepresented sequences, что не является критичным. Из отчета видим, что для Per sequence GC content распределение не идеально, но близко к нормальному. Главное, что Per base sequence quality полностью в норме. Basic statistics говорит что средний %GC составляет 48.
<p float='left'>
 <img width="500" alt="mod1" src="https://user-images.githubusercontent.com/91221560/156439028-25fbcabb-c8ff-4c67-818f-93324a9ff931.png">
 <img width="500" alt="mod2" src="https://user-images.githubusercontent.com/91221560/156439044-7d671129-654b-44b8-93ab-95516f66cf04.png">
 <img width="500" alt="mod3" src="https://user-images.githubusercontent.com/91221560/156439065-e71a2442-7935-4538-aa2c-70be6ef75bb1.png">
 <img width="500" alt="mod4" src="https://user-images.githubusercontent.com/91221560/156439081-7c943742-ee65-41d5-abcc-44d5f7aeb499.png">
</p>

*  2) Для ENCFF202SYS еще лучше показатели - все зеленые кроме одного оранжевого Overrepresented sequences, подрезать в данном случае не имеет смысла.
По картинке видим, что в Per tile sequence появился небольшой голубой прямоугольник, где качество хуже, но такие небольшие отклонения считаются в пределах нормы. Basic statistics снова показывает среднее GC содержание 48%.
<p float='left'>
  <img width="500" alt="sys1" src="https://user-images.githubusercontent.com/91221560/156466875-cdc688ad-24bd-4f8c-b491-b90efa60732b.png">
  <img width="500" alt="sys2" src="https://user-images.githubusercontent.com/91221560/156467199-770368d1-66e8-4eef-854e-30f5cd0f5c58.png">
  <img width="500" alt="sys3" src="https://user-images.githubusercontent.com/91221560/156467210-da953ee4-627f-4539-8e67-a4b56f8712c7.png">
  <img width="500" alt="sys4" src="https://user-images.githubusercontent.com/91221560/156467222-8e35175b-0d13-4c43-a589-0c9b58b404c0.png">
</p>

*  3) Для контроля ENCFF416GCS показатели хуже - два красных крестика Per tile sequence quality и Per base sequence content. В Per tile sequence quality видим много полосок не синего цвета, что говорит о плохом качестве, а в Per base sequence content видим, что на начальных позициях содержание C много меньше остальных, наибольшее у A и G. Здесь уже требовалось подрезание для улучшения качества, я провела обрезание с помощью trimmomatic, после чего стало немного лучше. Видно, что Per base sequence quality стало лучше, хотя и до этого был в пределе нормы, так же улучшился Per tile sequence quality - стало намного меньше полосок несинего цвета с плохим качеством.

До подрезаний:
<p float='left'>
  <img width="500" alt="gcs1" src="https://user-images.githubusercontent.com/91221560/156467946-9dc070bf-30e8-4ab9-bf9f-dbba7e786fa7.png">
  <img width="500" alt="gcs2" src="https://user-images.githubusercontent.com/91221560/156467977-c6a084d8-99c0-4cbe-9d68-45a616d6e2a7.png">
  <img width="500" alt="gcs3" src="https://user-images.githubusercontent.com/91221560/156467985-ed4e747f-a1c7-4288-97bc-29562f9975a4.png">
  <img width="500" alt="gcs4" src="https://user-images.githubusercontent.com/91221560/156467994-fd4399d6-1efb-42d4-843a-d05a7ff0285f.png">
</p>

После подрезаний:
<p float='left'>
  <img width="500" alt="Снимок экрана 2022-03-02 в 22 32 48" src="https://user-images.githubusercontent.com/91221560/156468163-f01f5e0e-bada-422f-ad44-6f786b9d7fa8.png">
  <img width="500" alt="Снимок экрана 2022-03-02 в 22 33 35" src="https://user-images.githubusercontent.com/91221560/156468178-641db348-6f0a-442c-a3a2-3c7ff0a00b42.png">
</p>

**Таблица**

<img width="722" alt="Снимок экрана 2022-03-03 в 02 49 19" src="https://user-images.githubusercontent.com/91221560/156469063-ceb27bcc-6366-4e25-8482-b24436f021a6.png">

Процент выравниваний как мы видим очень небольшой, что скорее всего связано с тем, что мы выравнивали только на одну хромосому 14 из-за того что ресурсы google colab ограничены для того, чтобы сделать это на все хромосомы.

 **Диаграммы Венна о пересечении наших MACS2 пиков и ENCODE пиков для двух реплик**
 *  Для реплик ENCFF974MOD и ENCFF202SYS с параметром --broad получилось совсем маленькое пресечение с ENCODE пиками:
<p float='left'>
 <img width="500" alt="Снимок экрана 2022-03-03 в 10 58 37" src="https://user-images.githubusercontent.com/91221560/156521722-a74a57cd-35e9-4f7f-8cbc-32d1fbfd5621.png">
 <img width="500" alt="Снимок экрана 2022-03-03 в 10 57 46" src="https://user-images.githubusercontent.com/91221560/156521776-d96b96c9-7761-4523-960d-91a9458c72cd.png">
 <img width="500" alt="Снимок экрана 2022-03-03 в 10 58 58" src="https://user-images.githubusercontent.com/91221560/156521796-a2db0208-62b8-4b68-9a57-5778548e2807.png">
 <img width="500" alt="Снимок экрана 2022-03-03 в 10 59 16" src="https://user-images.githubusercontent.com/91221560/156521813-3f40615f-f061-4830-86f8-fea68ab4bd4e.png">
</p>

* Поэтому я решила изменить параметр, так как пики сильно зависят от параметров - попробовала вместо --broad: --nolambda и пересечений стало заметно больше:
<p float='left'>
 <img width="500" alt="Снимок экрана 2022-03-03 в 11 03 44" src="https://user-images.githubusercontent.com/91221560/156522601-d576284a-5a5c-42e7-9899-4b9311ab3346.png">
 <img width="500" alt="Снимок экрана 2022-03-03 в 11 04 13" src="https://user-images.githubusercontent.com/91221560/156522615-460b8813-ab0c-4319-aac4-9fa7582afc43.png">
 <img width="500" alt="Снимок экрана 2022-03-03 в 11 04 37" src="https://user-images.githubusercontent.com/91221560/156522632-5fbbefc3-0474-4c8b-a2a9-24e8c08ef419.png">
 <img width="500" alt="Снимок экрана 2022-03-03 в 11 04 59" src="https://user-images.githubusercontent.com/91221560/156522662-dbd6f689-dd18-4f94-9b5a-a3d25d46f220.png">
</p>

Сравнивая те пики, которые мы получили, с пиками, которые приведены в ENCODE, видим, что пересечение не очень большое, что опять же связано с тем, что у нас выравнивание приходилось только на одну небольшую хромосому 14, а в ENCODE - на все хромосомы, поэтому и пиков там намного больше.
Различия в количестве пересечений когда мы меняем местами encode и наш файл объясняется тем, что в первом случае мы смотрим на те участки из файла ENCODE, которые пересекаются с нашим файлом, а во втором случае наоборот смотрим на участки нашего файла, которые пересекаются с ENCODE. Следующая картинка хорошо визуализирует данные различия:

<img width="777" alt="Снимок экрана 2022-03-08 в 20 26 31" src="https://user-images.githubusercontent.com/91221560/157293643-9fe7eeea-6c47-4af9-b703-004c207eb99b.png">

**БОНУС**
Получился такой NGS-plot для сайта посадки гистоновой метки:

для bigwig файлов ENCFF672IAE и ENCFF749GHM, соответсвующие bam файлам ENCFF242PMY.bam и ENCFF098OBN.bam, слева общий вид, а справа приближены первые строчки heatmap, где лучше видны характерные особенности.
<p float='left'>
 <img width="250" alt="Снимок экрана 2022-03-03 в 13 44 08" src="https://user-images.githubusercontent.com/91221560/156549305-3dc35dd5-f97a-44db-a69a-f7d6c2649d47.png">
 <img width="600" alt="Снимок экрана 2022-03-08 в 19 22 26" src="https://user-images.githubusercontent.com/91221560/157280852-01dd7b21-d7a1-4134-99ba-2f41cd726551.png">
  
 <img width="250" alt="Снимок экрана 2022-03-08 в 19 21 11" src="https://user-images.githubusercontent.com/91221560/157281109-f7a3ed85-6fd3-451a-82c8-29acfccece6c.png">

 <img width="600" alt="Снимок экрана 2022-03-08 в 19 21 53" src="https://user-images.githubusercontent.com/91221560/157281146-4a56ed89-ea94-482a-afd2-b9d2b7dcb16c.png">
</p>

Достаточно отчетливо видно, что почти на каждом гене (1ген=1строчка) более насыщенный (чем темнее, тем больше чтений) цвет приходится на участок, который немного левее и правее начала транскрипции (TSS), что подтверждает график сверху - там изображено усреднение по столбцам - видим, что пик приходится на позицию чуть раньше TSS и чуть позже. На первых нескольких строчках heatmap видим, что насыщенный цвет на протяжение всего участка от TSS до TES, но число таких генов как иллюстрирует карта ничтожно мало. Так же интересно заметить, что минимум достигается на отметке TES, то есть там меньше всего вероятность, что будет присутствовать гистоновая метка, можно предположить, что там доступность хроматина ниже и поэтому белок не может присоединиться(видно по графику с усреднениями по столбцам). Касаемо участка +2000 bp после TES - усреденение показывает, что там примерно столько же чтений (немного), сколько и в промежутке между TSS и TES.

То что пик находится примерно в районе TSS согласуется с тем что получилось в статье:
<img width="548" alt="Снимок экрана 2022-03-08 в 19 37 03" src="https://user-images.githubusercontent.com/91221560/157283698-bf922517-c525-43ee-82a1-b9313b70037c.png">

Информация из википедии: H4K8ac is part of 17 modifications of a group of active promoters. H4K8ac is found more often in active promoters and transcribed regions than other marks.
