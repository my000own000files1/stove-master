# stove

**По-русски** | [In english](docs_eng/README.md)

## РАЗРАБОТКА МАКЕТА ПРОГРАММНО-АППАРАТНОГО КОМПЛЕКСА ДЛЯ УПРАВЛЕНИЯ ТЕМПЕРАТУРОЙ В ПЕЧАХ ДЛЯ ВАРКИ СТЕКЛА НА ОСНОВЕ МИКРОКОНТРОЛЛЕРА ATMEGA2560

### Аннотация 
В статье рассматривается разработка макета программно-аппаратного комплекса
 для управления температурой в печах для варки стекла на основе микроконтроллера ATmega2560. 
 Для контроля и поддержания температуры в камере печи использован алгоритм с ПИ-регулятором,
 который управляет симисторной сборкой для подачи киловаттной мощности на рассеивающий тепло
 элемент печи. Обратная связь осуществляется посредством оцифровки сигнала с термопары микросхемой 
 CJMCU-MAX31856. 
Для ввода/вывода информации был разработан пользовательский интерфейс на основе TFT дисплея Nextion. 

[Закладки, которые использовались при выполгнении проекта.](/docs/stove_bookmarks.md)

Проект был представлен на 
[VII Научно-практической конференции «Наука настоящего и будущего» 2019](https://nnb.etu.ru/postupayushhim-v-magistraturu/konferencii-predydushhih-let/vii-nauchno-prakticheskaya-konferenciya-nauka-nastoyashhego-i-budushhego-2019).

Непосредственно сам доклад находится на стр.75-78 [здесь](https://nnb.etu.ru/assets/files/rezultaty/mag/2019/tom_1_finn.pdf "Сборник материалов конференции16 – 18 мая 2019 1 Том ") 
или [здесь](/docs/report.pdf "вырезанный").

[Файлы, которые отправлялись на конференцию](/docs "открыть папку"):
1. [Доклад в формате pdf](/docs/report_full.pdf)
1. [Доклад в формате WORD](/docs/report_full.docx "открыть")
1. [Презентация доклада в формате ppt](/docs/presentation.ppt "открыть")
1. [Презентация доклада в формате pdf](/docs/presentation.pdf "открыть")

Дополнительные файлы с информацией о проекте:
1. [Доклад для сдачи дисциплины "Микропроцессорные устройства систем управления" в формате pdf](/docs/report_for_university.pdf)
1. [Доклад для сдачи дисциплины "Микропроцессорные устройства систем управления" в формате WORD](/docs/report_for_university.docx)
1. [Алгоритм подбора коэффициентов ПИД-регулятора](docs/PID_coeff_choose.php)
1. Рукописные наброски псевдокода и размышления на листе:
	1. Подбор коэффициентов ПИД-регулятора [1](docs/pseudo-code_handwritten_outline/PIR_setting1.pdf),[2](docs/pseudo-code_handwritten_outline/PIR_setting2.pdf)
	1. [Отправка данных целевой функции на MCU с Nextion (SD-card)](docs/pseudo-code_handwritten_outline/sending_target_function_data.pdf)
	2. [Структурная схема модели САУ](docs/pseudo-code_handwritten_outline/ACS_model.pdf)
	3. [Установка точек на дисплее Nextion](docs/pseudo-code_handwritten_outline/setting_point_on_Nextion.pdf)
	4. [Сколько памяти занимают компоненты variable](docs/pseudo-code_handwritten_outline/var_length_in_memory.pdf)
1.  [Примеры реализации расчте показателей качества для переходной характеристики в MATLAB](examples/matlab_stepinfo/)	
	
Картинки с фотографиями [находятся здесь](docs/images)

1. Главный алгоритм изображен в виде блок-схемы в программе draw.io здесь [main_loop.html](https://app.diagrams.net/#G1erNzenc1y8jMb31vDRvs-M2VeMvLVpRX) 


Видео с демонстрацией работы находятся на хостинге youtube:

В видео демонстриуется работа интерфейса дисплея.

<a href="http://www.youtube.com/watch?feature=player_embedded&v=TroMaXGrYXM" target="_blank"><img src="http://img.youtube.com/vi/TroMaXGrYXM/0.jpg" 
alt="ALT-ТЕКСТ ИЗОБРАЖЕНИЯ" width="192" height="144" border="10" /></a>

 Одновременно с этим можно видеть две основные проблемы:
1. Во время слежения за температурой, когда значение температуры превышает 512 градусов, переменная  переполняется 
и температура начинает отсчитываться от нуля, алгоритм "думает", что температура очень низкая и происходит фатальная 
ошибка, которая приводит к резкому нагреву.
2. Микроконтроллер зависает по истечению определенного времени. Я пришел к такому выводу, 
потому что данные на дисплее не обновляются erg
и их также невозможно изменить командами с дисплея. 

### <img src="https://github.com/my000own000files1/stove-master/blob/master/docs/images/icon.png" alt="anonymous" />  Структура программы:

Программа была написана на языке "C" в Arduino IDE. [Примеры, которые использовались во время выполнения проекта.](examples/README.md)

В [этой папке](/libraries) находятся библиотеки, необходимые для компиляции основного файла.
Основная программа для компиляции [stove.ino](/stove.ino)

Документация на дисплей [здесь](components/nextion_docs/The_Nextion_Editor_Guide_trans.pdf)
Программа для дисплея Nextion была написана на специальном языке. Инструкции описаны в [этом документе](components/nextion_docs/istruction_set_trans.pdf).
Все файлы по работе интерфейса находятся в папке [HMI_Nextion](/HMI_Nextion). 

1. [Техническое задание на интерфейс](HMI_Nextion/TT_interface.pdf)
2. [Программа для компиляции - stove.HMI](HMI_Nextion/stove.HMI)
3. [Приблизительный дизайн интерфейса](HMI_Nextion/images_for_HMI/first_interface.jpg)
