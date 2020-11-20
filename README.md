# Торговые точки вблизи ТПУ, г.Москва

<img align="right" width="100" height="100" src="https://i.ibb.co/TbyCPm8/logoza-ru-1.png">

## Команда «Data SkyScrapers»

\
ФИЛИППЕНКО Артем, ГАБИТОВ Ильдар, КАНДЫБИН Вячеслав,  КОМПАНИЕЦ Юлия, ПЕТРОВ Егор


## Описание датасета

В датастете содержится информация о торговых объектах и ближайших к ним транспортно-пересадочных узлов в г. Москва с указанием эффективной зоны охвата объекта. Кроме того в датасете содержится следующая информация:

* Данные о стоимости коммерческой недвижимости в районе объекта
* Демографические и географические данные о районе объекта
* Данные о зоне охвата объекта
* Данные о пассажиропотоке ближайшей станции метро

Часть данных в датасете представлена в виде словарей, что связано с вложенностью отдельных признаков. К примеру, ряд ТПУ представляют собой комплекс из отдельных объектов наземного и подземного транспорта.

Датасет может быть использован для выбора места расположения новой торговой точки по критерию "наиболее благоприятные условия". 
Преимущество датасета состоит в том, что но актуален на настоящее время, содержит официальные данные и множество дополнительных характеристик.


<img align="center" src="https://i.ibb.co/3sMqBY2/map.png"> <img align="center" src="https://i.ibb.co/3sMqBY2/map.png">

## Источники

В датасете были использованы следующие данные с сайта [Портал открытых данных](https://data.mos.ru) города Москва:

* [Транспортно-пересадочные узлы](https://data.mos.ru/opendata/7704786030-transportno-peresadochnye-uzly?pageNumber=1&versionNumber=4&releaseNumber=27)
* [Стационарные торговые объекты](https://data.mos.ru/opendata/7710881420-statsionarnye-torgovye-obekty?pageNumber=1&versionNumber=1&releaseNumber=22)
* [Бытовые услуги на территории Москвы](https://data.mos.ru/opendata/7710881420-bytovye-uslugi-na-territorii-moskvy/data/table?versionNumber=2&releaseNumber=30)

Другие источники:
<br/> 
 * Расчет торговой зоны и зоны охвата магазина был произведен на основе статьи ["Расчет торговой зоны и зоны охвата магазина"](http://www.arhitrade.com/education.php?Id=43)
 * Информация о районах: [Wikipedia: Список районов и поселений Москвы](https://ru.wikipedia.org/wiki/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D1%80%D0%B0%D0%B9%D0%BE%D0%BD%D0%BE%D0%B2_%D0%B8_%D0%BF%D0%BE%D1%81%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D0%B9_%D0%9C%D0%BE%D1%81%D0%BA%D0%B2%D1%8B)
 * Информация о ценах на коммерческую недвижимость: [Restate](https://msk.restate.ru/graph/ceny-arendy-kommercheskoy/)
 * Сведения о пассажиропотоке на станциях: [Рекламное агентство Метро Москвы](https://www.metro-msk.ru/stat/2019/)
 * [Геоданные](http://gis-lab.info/data/mos-adm/mo.geojson) о форме административных районов и округов Москвы

## Методы сбора и обработки

В качестве основы датасета были взяты данные с сайта [Портал открытых данных](https://data.mos.ru), и далее собраны в единый датасет с применением библиотеки **pandas**. <br/> 
Для сбора данных по зонам охвата магазинов, информации о пассажиропотоке и данных по районам г.Москвы были использованны методы парсинга с применением библиотек **requests**, **lxml** и **BeautifulSoup**.
Таблица о стоимости аренды и покупки недвижимости по районам была методом ручного парсинга сайта [Restate](https://msk.restate.ru/graph/ceny-arendy-kommercheskoy/) <br/> 
Для визуализации объектов на карте была использована библиотека **[Folium](https://python-visualization.github.io/folium/index.html)**.

## Структура репозитория


    .                   
    ├── data                             # промежуточные датасеты
    │   ├── realty_cost.xlsx             # стоимость аренды и покупки помещения, г.Москва       
    │   ├── tpu.xlsx                     # информация о ТПУ, г.Москва     
    │   ├── trade_place_tpu.csv          # промежуточная таблица принадлежности торгового объекта к ТПУ  
    │   ├── Бытовые услуги.xlsx          # информация о торговых точках, г.Москва
    │   └── стационарные объекты.xlsx    # информация о торговых точках, г.Москва              
    ├── data_example.json                # структура датасета в формате json
    ├── 02_team_hak_19_10_data_gathering.ipynb # ноутбук блок сбора данных
    ├── 02_team_hak_19_10_visualisation.ipynb # ноутбук блок визуализации
    └── README.md

Весь код тестировался только Google Colab, поэтому гарантировать корректную работу в других приложениях мы не можем.
Ноутбук был разделен на две части: непосредственный сбор данных и блок с визуализацией.

## Структура датасета

Ссылка на датасет: [Google Drive](https://drive.google.com/file/d/179ShmAMQsWjTCGHWthf75jCD1lh7WPLC/view?usp=sharing)

Датасет состоит из 44 столбцов и 78086 строк. <br/> 
Объем занимаемой памяти: 25.9+ MB.

Список используемых сокращений:
* **ТО** - торговый объект
* **ТПУ** - транспортно-пересадочный узел

|№| **Название** | **Описание** | **Тип** | **Кол-во NaN значений** | **Значения** |
| ------ | ------ | ------ | ------ | ------ | ------ |
| 1 | **object_global_id** | id ТО | int | 0 | |
| 2 | **object_name** | Название ТО| str | 0 | |
| 3 | **is_network_object** | Является ли ТО сетевым | int | 0 | 0 = не сетевой объект, <br/> 1 = сетевой объект |
| 4 | **is_tpu_in_coverage** | Находится ли ТО в зоне покрытия ТПУ | int | 0 | 0 = нет, <br/> 1 = да |
| 5 | **object_operating_company** | Управляющая компания ТО | str | 58351 |  |
| 6 | **object_service_type** | Тип предоставляемой услуги ТО | str | 0 | |
| 7 | **object_type** | Тип ТО  | str | 0 | |
| 8 | **object_area** | Административный округ ТО| str | 0 | |
| 9 | **object_district** | Район ТО | str| 0 | |
| 10 | **object_address** | Адрес ТО | str | 0 | |
| 11 | **object_phone** | Номер телефона ТО | str | 0 | |
| 12 | **object_working_hours** | Время работы ТО | dict | 0 | |
| 13 | **object_working_hours_clarification** | Уточнение времени работы ТО | str | 77996 | |
| 14 | **object_size** | Размер ТО | int | 0 | 1 = маленький, <br/> 2 = средний, <br/>  3 = большой |
| 15 | **object_longitude** | Координаты расположения ТО: долгота | float | 0 | |
| 16 | **object_latitude** | Координаты расположения ТО: широта | float | 0 | |
| 17 | **object_real_reach_distance** | Зона охвата ТО | float | 0 | 2000.0, 4000.0, 10000.0 |
| 18 | **distance_to_tpu** | Расстояния от ТО до ближайшего ТПУ, метры | float | 0 | |
| 19 | **tpu_name** | Название ТПУ | str | 0 | |
| 20 | **tpu_global_id** | id ТПУ | float | 0 | |
| 21 | **tpu_content** | id включенных станций ТПУ | dict | 0 | |
| 22 | **tpu_content_count** | кол-во включенных станций ТПУ | int | 0 | |
| 23 | **tpu_district** | Район, в котором находится ТПУ | dict | 0 | | 
| 24 | **tpu_near_station** | Ближайшая к ТПУ станция| str | 0 | |
| 25 | **tpu_comissioning_year** | Год сдачи ТПУ в эксплуатацию | float | 0 | |
| 26 | **tpu_status** | Статус ТПУ | str | 0 | проект, построен, строится, частично построен |
| 27 | **tpu_available_transfer**| Доступные виды трансфера ТПУ | str | 3577 | |
| 28 | **tpu_car_capacity** | Количество машино-мест возле ТПУ | float | 41795 | |
| 29 | **tpu_longitude** | Координаты расположения ТПУ: долгота | dict | 0 | |
| 30 | **tpu_latitude** | Координаты расположения ТПУ: широта | dict | 0 | |
| 31 | **subway_station** | Ближайшая станция метро | str | 11093 | |
| 32 | **subway_line** | Линия ближайшей станции метро | str | 19652 | |
| 33 | **subway_passengers_per_day** | Пассажиропоток ближайшей станции метро | float | 20765 | |
| 34 | **object_district_square_m2** | Площадь района, в котором находится ТО, м2 | float | 19253 | |
| 35 | **object_district_population** | Население района, в котором находится ТО | float | 19253 | |
| 36 | **object_district_population_density** | Плотность населения района, в котором находится ТО | float | 19253 | |
| 37 | **object_district_living_space_m2** | Площадь жилого фонда района, в котором находится ТО | float | 19253 | |
| 38 | **object_district_living_space_m2_per_person** | Жилплощадь на человека района, в котором находится ТО | float | 19253 | |
| 39 | **object_district_building_property_price_per_m2** | Цена продажи м2 здания для района, в котором находится ТО | float | 67783 | |
| 40 | **object_district_tradeplace_property_price_per_m2** | Цена продажи м2 торгового помещения для района, в котором находится ТО | float  | 33607 | |
| 41 | **object_district_generalplace_property_price_per_m2** | Цена продажи м2 помещения свободного назначения для района, в котором находится ТО | float | 29913 | |
| 42 | **object_district_building_rent_price_per_m2** | Цена аренды м2 здания для района, в котором находится ТО | float | 65302 | |
| 43 | **object_district_tradeplace_rent_price_per_m2**| Цена аренды м2 торгового помещения для района, в котором находится ТО | float | 23483 | |
| 44 | **object_district_generalplace_rent_price_per_m2**| Цена аренды м2 помещения свободного назначения для района, в котором находится ТО | float | 19668 | |


