# hse_hw2_chip
* C помощью анализа ChIP-Seq данных определим участки, где есть конкретная гистоновая модификация в заданном типе клеток.
*  Я взяла клеточную линию H9 и гистоновую метку H4K8ac.

**Отчеты Fastqc:**
*  1) Для ENCFF974MOD все харатеристики оказались в норме, все зеленые галочки кроме двух оранжевых Per sequence GC content и Overrepresented sequences, что не является критичным.
<p float='left'>
 <img width="500" alt="mod1" src="https://user-images.githubusercontent.com/91221560/156439028-25fbcabb-c8ff-4c67-818f-93324a9ff931.png">
 <img width="500" alt="mod2" src="https://user-images.githubusercontent.com/91221560/156439044-7d671129-654b-44b8-93ab-95516f66cf04.png">
 <img width="500" alt="mod3" src="https://user-images.githubusercontent.com/91221560/156439065-e71a2442-7935-4538-aa2c-70be6ef75bb1.png">
 <img width="500" alt="mod4" src="https://user-images.githubusercontent.com/91221560/156439081-7c943742-ee65-41d5-abcc-44d5f7aeb499.png">
</p>

*  2) Для ENCFF202SYS еще лучше показатели - все зеленые кроме одного оранжевого Overrepresented sequences, подрезать в данном случае не имеет смысла.
<p float='left'>
  <img width="500" alt="sys1" src="https://user-images.githubusercontent.com/91221560/156466875-cdc688ad-24bd-4f8c-b491-b90efa60732b.png">
  <img width="500" alt="sys2" src="https://user-images.githubusercontent.com/91221560/156467199-770368d1-66e8-4eef-854e-30f5cd0f5c58.png">
  <img width="500" alt="sys3" src="https://user-images.githubusercontent.com/91221560/156467210-da953ee4-627f-4539-8e67-a4b56f8712c7.png">
  <img width="500" alt="sys4" src="https://user-images.githubusercontent.com/91221560/156467222-8e35175b-0d13-4c43-a589-0c9b58b404c0.png">
</p>

*  3) Для контроля ENCFF416GCS показатели хуже - два красных крестика Per tile sequence quality и Per base sequence content, поэтому я провела обрезание с помощью trimmomatic, после чего стало немного лучше.

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

**БОНУС**
Получился такой NGS-plot для сайта посадки белка:

<img width="200" alt="Снимок экрана 2022-03-03 в 13 44 08" src="https://user-images.githubusercontent.com/91221560/156549305-3dc35dd5-f97a-44db-a69a-f7d6c2649d47.png">

Достаточно отчетливо видно, что почти на каждом гене (1ген=1строчка) более насыщенный (чем темнее, тем больше чтений) цвет приходится на участок начала (TSS), что подтверждает график сверху - там изображено усреднение по столбцам - видим, что пик приходится на TSS. На первых нескольких строчках heatmap видим, что насыщенный цвет на протяжение всего участка от TSS до TES, но число таких генов как иллюстрирует карта ничтожно мало. Так же интересно заметить, что минимум достигается на отметке TES, то есть там меньше всего вероятность, что будет присутсвовать гистоновая метка (видно по графику с усреднениями по столбцам). Касаемо участков +-2000 нуклеотидов до TSS и после TES - усреденение показывает, что там примерно столько же чтений (немного), сколько и в промежутке между TSS и TES.
