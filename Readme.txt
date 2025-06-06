# Проект "Базы данных"

Проект представляет собой создание, наполнение и манипуляцию данными в БД MySQL.
Целью проекта является закрепление полученных в курсе Базы данных знаний.

В проекте представлены 4 различные базы данных:
- транспортные средства;
- автомобильные гонки;
- бронирование отелей;
- структура организации.

Каждая из баз данных включает в себя этапы создания таблиц, наполнения их данными, а также решение задач разной сложности.

Каждая из представленных баз данных сопровождается скриптом, который создает таблицы базы данных и заполняет их тестовыми данными.

## База данных 1. Транспортные средства.

### Условие.

Структура базы данных включает три таблицы для хранения информации о различных типах транспортных средств:
Vehicle, Car, Motorcycle и Bicycle. Каждая таблица имеет свои уникальные атрибуты и взаимосвязи.

#### 1. Таблица `Vehicle`
- Цель: Содержит общую информацию о производителях и моделях транспортных средств.
- Поля:
    - `maker`: (VARCHAR) Название производителя автомобиля или мотоцикла.
    - `model`: (VARCHAR) Название модели. Это поле также служит первичным ключом, что означает, что каждая модель должна быть уникальной.
    - `type`: (ENUM) Тип транспортного средства, который может принимать одно из значений: 'Car', 'Motorcycle', 'Bicycle'.

#### 2. Таблица `Car`
- Цель: Содержит детали о легковых автомобилях.
- Поля:
    - `vin`: (VARCHAR) Уникальный идентификатор автомобиля (номер VIN), который является первичным ключом.
    - `model`: (VARCHAR) Название модели автомобиля, которая ссылается на поле `model` в таблице `Vehicle`. Это поле используется как внешний ключ для обеспечения целостности данных.
    - `engine_capacity`: (DECIMAL) Объем двигателя в литрах.
    - `horsepower`: (INT) Мощность двигателя в лошадиных силах.
    - `price`: (DECIMAL) Цена автомобиля в долларах.
    - `transmission`: (ENUM) Тип трансмиссии, которая может быть 'Automatic' (автоматическая) или 'Manual' (механическая).

#### 3. Таблица `Motorcycle`
- Цель: Содержит детали о мотоциклах.
- Поля:
    - `vin`: (VARCHAR) Уникальный идентификатор мотоцикла (номер VIN), который является первичным ключом.
    - `model`: (VARCHAR) Название модели мотоцикла, которая ссылается на поле `model` в таблице `Vehicle`, используется как внешний ключ.
    - `engine_capacity`: (DECIMAL) Объем двигателя в литрах.
    - `horsepower`: (INT) Мощность двигателя в лошадиных силах.
    - `price`: (DECIMAL) Цена мотоцикла в долларах.
    - `type`: (ENUM) Тип мотоцикла, который может принимать одно из значений: 'Sport', 'Cruiser', 'Touring'.

#### 4. Таблица `Bicycle`
- Цель: Содержит детали о велосипедах.
- Поля:
    - `serial_number`: (VARCHAR) Уникальный серийный номер велосипеда, который является первичным ключом.
    - `model`: (VARCHAR) Название модели велосипеда, которая ссылается на поле `model` в таблице `Vehicle`, используется как внешний ключ.
    - `gear_count`: (INT) Количество передач велосипеда.
    - `price`: (DECIMAL) Цена велосипеда в долларах.
    - `type`: (ENUM) Тип велосипеда, который может принимать одно из значений: 'Mountain', 'Road', 'Hybrid'.

#### Взаимосвязи
- Каждая из таблиц `Car`, `Motorcycle` и `Bicycle` ссылается на таблицу `Vehicle` через поле `model`, что обеспечивает целостность данных. Это значит, что каждая модель, указанная в таблицах `Car`, `Motorcycle` и `Bicycle`, должна предварительно существовать в таблице `Vehicle`.
- Таблицы `Car`, `Motorcycle` и `Bicycle` можно считать подмножествами таблицы `Vehicle`, где каждая подтаблица содержит специфические детали для каждого типа транспортного средства.

Данная структура базы данных организует информацию о транспортных средствах в соответствии с их типами и основными характеристиками. Она позволяет удобно хранить, просматривать и поддерживать данные о различных моделях автомобилей, мотоциклов и велосипедов, сохраняя при этом их связь с производителями.

### Подготовительный этап:
1. Создадим БД vehicles в графическом интерфейсе.
2. Создадим таблицы, запустив скрипт из файла databases/vehicles/V1__create_tables.sql.
3. Наполним таблицы данными с помощью скрипта databases/vehicles/V2__insert_data.sql.

### Задачи:
#### Задача 1.
Условие:
Найдите производителей (maker) и модели всех мотоциклов, которые имеют мощность более 150 лошадиных сил,
стоят менее 20 тысяч долларов и являются спортивными (тип Sport). Также отсортируйте результаты
по мощности в порядке убывания.

Решение:
размещено в скрипте databases/vehicles/V3__task1.sql.

#### Задача 2.
Условие:
Найти информацию о производителях и моделях различных типов транспортных средств
(автомобили, мотоциклы и велосипеды), которые соответствуют заданным критериям.

Автомобили:
Извлечь данные о всех автомобилях, которые имеют:

Мощность двигателя более 150 лошадиных сил.
Объем двигателя менее 3 литров.
Цену менее 35 тысяч долларов.
В выводе должны быть указаны производитель (maker), номер модели (model),
мощность (horsepower), объем двигателя (engine_capacity)
и тип транспортного средства, который будет обозначен как Car.

Мотоциклы:
Извлечь данные о всех мотоциклах, которые имеют:

Мощность двигателя более 150 лошадиных сил.
Объем двигателя менее 1,5 литров.
Цену менее 20 тысяч долларов.
В выводе должны быть указаны производитель (maker), номер модели (model),
мощность (horsepower), объем двигателя (engine_capacity)
и тип транспортного средства, который будет обозначен как Motorcycle.

Велосипеды:
Извлечь данные обо всех велосипедах, которые имеют:

Количество передач больше 18.
Цену менее 4 тысяч долларов.
В выводе должны быть указаны производитель (maker), номер модели (model),
а также NULL для мощности и объема двигателя, так как эти характеристики
не применимы для велосипедов. Тип транспортного средства будет обозначен как Bicycle.

Сортировка:
Результаты должны быть объединены в один набор данных и отсортированы
по мощности в порядке убывания. Для велосипедов,
у которых нет значения мощности, они будут располагаться внизу списка.

Решение:
размещено в скрипте databases/vehicles/V4__task2.sql.


## База данных 2. Автомобильные гонки.

### Условие
Структура базы данных включает в себя четыре основные таблицы, которые организуют информацию о классе автомобилей, самих автомобилях, гонках и результатах гонок. Рассмотрим каждую из таблиц детальнее:

#### 1. Таблица `Classes`
- Цель: Хранит информацию о различных классах автомобилей.
- Поля:
    - `class`: (VARCHAR) Название класса автомобилей, который служит первичным ключом и должен быть уникальным для каждого класса.
    - `type`: (ENUM) Тип класса, который может принимать значения 'Racing' или 'Street', определяющие назначения автомобилей.
    - `country`: (VARCHAR) Страна, с которой связан этот класс автомобилей.
    - `numDoors`: (INT) Количество дверей в автомобиле данного класса.
    - `engineSize`: (DECIMAL) Размер двигателя в литрах, с точностью до одного знака после запятой.
    - `weight`: (INT) Вес автомобиля в килограммах.

#### 2. Таблица `Cars`
- Цель: Хранит информацию об автомобилях.
- Поля:
    - `name`: (VARCHAR) Название автомобиля, которое служит первичным ключом и должно быть уникальным.
    - `class`: (VARCHAR) Название класса, к которому принадлежит автомобиль. Это поле используется как внешний ключ, ссылающийся на поле `class` в таблице `Classes`. Это обеспечивает целостность данных, гарантируя, что каждый автомобиль относится к существующему классу.

#### 3. Таблица `Races`
- Цель: Хранит информацию о гонках.
- Поля:
    - `name`: (VARCHAR) Название гонки, которое служит первичным ключом и должно быть уникальным.
    - `date`: (DATE) Дата проведения гонки, что позволяет сохранить информацию о времени гонки.

#### 4. Таблица `Results`
- Цель: Хранит результаты гонок для автомобилей.
- Поля:
    - `car`: (VARCHAR) Название автомобиля, который участвовал в гонке. Это поле используется как внешний ключ, ссылающийся на поле `name` в таблице `Cars`.
    - `race`: (VARCHAR) Название гонки, в которой участвовал автомобиль. Это поле используется как внешний ключ, ссылающийся на поле `name` в таблице `Races`.
    - `position`: (INT) Позиция, которую автомобиль занял в гонке. Это число указывает на успешность участия автомобиля в конкретной гонке.
    - Пара (car, race) образует первичный ключ, гарантируя уникальность каждой записи в таблице результатов, так как один автомобиль не может участвовать в одной гонке более одного раза.

#### Взаимосвязи
- Таблица `Cars` ссылается на таблицу `Classes`, обеспечивая связку между автомобилями и их классами.
- Таблица `Results` связывает автомобили с гонками, предоставляя информацию о том, какое место занял каждый автомобиль в конкретной гонке. Ссылки на таблицы `Cars` и `Races` обеспечивают целостность и согласованность данных.

Данная структура базы данных организует и систематизирует информацию о классах автомобилей, самих автомобилях, гонках и их результатах. Она позволяет удобно хранить и обрабатывать данные о гоночных классах, автомобилях и их участии в гонках, сохраняя при этом целостность и связь между записями.

### Подготовительный этап:
1. Создадим БД car_races в графическом интерфейсе.
2. Создадим таблицы, запустив скрипт из файла databases/car_races/V1__create_tables.sql.
3. Наполним таблицы данными с помощью скрипта databases/car_races/V2__insert_data.sql.

### Задачи:
#### Задача 1.
Условие:
Определить, какие автомобили из каждого класса имеют наименьшую среднюю позицию в гонках,
и вывести информацию о каждом таком автомобиле для данного класса, включая его класс,
среднюю позицию и количество гонок, в которых он участвовал.
Также отсортировать результаты по средней позиции.

Решение:
размещено в скрипте databases/car_races/V3__task1.sql.

#### Задача 2.
Условие:
Определить автомобиль, который имеет наименьшую среднюю позицию в гонках среди всех автомобилей,
и вывести информацию об этом автомобиле, включая его класс, среднюю позицию, количество гонок,
в которых он участвовал, и страну производства класса автомобиля.
Если несколько автомобилей имеют одинаковую наименьшую среднюю позицию,
выбрать один из них по алфавиту (по имени автомобиля).

Решение:
размещено в скрипте databases/car_races/V4__task2.sql.

#### Задача 3.
Условие:
Определить классы автомобилей, которые имеют наименьшую среднюю позицию в гонках,
и вывести информацию о каждом автомобиле из этих классов, включая его имя,
среднюю позицию, количество гонок, в которых он участвовал, страну производства
класса автомобиля, а также общее количество гонок, в которых участвовали
автомобили этих классов.
Если несколько классов имеют одинаковую среднюю позицию, выбрать все из них.

Решение:
размещено в скрипте databases/car_races/V5__task3.sql.

#### Задача 4.
Условие:
Определить, какие автомобили имеют среднюю позицию лучше (меньше) средней позиции
всех автомобилей в своем классе (то есть автомобилей в классе должно быть минимум два,
чтобы выбрать один из них). Вывести информацию об этих автомобилях, включая их имя,
класс, среднюю позицию, количество гонок, в которых они участвовали, и
страну производства класса автомобиля.
Также отсортировать результаты по классу и затем по средней позиции в порядке возрастания.

Решение:
размещено в скрипте databases/car_races/V6__task4.sql.

#### Задача 5.
Условие:
Определить, какие классы автомобилей имеют наибольшее количество автомобилей с
низкой средней позицией (больше 3.0) и вывести информацию о каждом автомобиле
из этих классов, включая его имя, класс, среднюю позицию, количество гонок,
в которых он участвовал, страну производства класса автомобиля, а также
общее количество гонок для каждого класса. Отсортировать результаты по
количеству автомобилей с низкой средней позицией.

Решение:
размещено в скрипте databases/car_races/V7__task5.sql.

## База данных 3. Бронирование отелей.

### Условие.
Структура базы данных предназначена для управления информацией о гостиницах, номерах, клиентах и бронированиях. Она состоит из четырех таблиц: `Hotel`, `Room`, `Customer` и `Booking`. Рассмотрим каждую таблицу подробнее.

#### 1. Таблица `Hotel`
- Цель: Хранит информацию о гостиницах.
- Поля:
    - `ID_hotel`: (INT) Уникальный идентификатор гостиницы, который служит первичным ключом. Этот идентификатор должен быть уникальным для каждой записи в таблице.
    - `name`: (VARCHAR) Название гостиницы. Это обязательное поле, которое не может быть пустым.
    - `location`: (VARCHAR) Местоположение гостиницы. Это также обязательное поле, не допускающее пустых значений.

#### 2. Таблица `Room`
- Цель: Хранит информацию о номерах в гостиницах.
- Поля:
    - `ID_room`: (INT) Уникальный идентификатор номера, который служит первичным ключом и должен быть уникальным для каждого номера.
    - `ID_hotel`: (INT) Идентификатор гостиницы, к которой принадлежит номер. Это поле используется как внешний ключ, ссылающийся на `ID_hotel` в таблице `Hotel`, что обеспечивает связь между номерами и гостиницами.
    - `room_type`: (ENUM) Тип номера, который может принимать значения 'Single', 'Double' или 'Suite', указывая на тип размещения.
    - `price`: (DECIMAL) Цена номера за ночь, представлена с точностью до двух знаков после запятой.
    - `capacity`: (INT) Вместимость номера, то есть максимальное количество людей, которые могут разместиться в данном номере.

#### 3. Таблица `Customer`
- Цель: Хранит информацию о клиентах гостиницы.
- Поля:
    - `ID_customer`: (INT) Уникальный идентификатор клиента, который служит первичным ключом. Этот идентификатор должен быть уникальным.
    - `name`: (VARCHAR) Имя клиента. Это обязательное поле, которое не может быть пустым.
    - `email`: (VARCHAR) Электронная почта клиента. Это обязательное поле, и его значения должны быть уникальными, чтобы избежать дубликатов. Оно не может быть пустым.
    - `phone`: (VARCHAR) Номер телефона клиента. Это обязательное поле, не допускающее пустых значений.

#### 4. Таблица `Booking`
- Цель: Хранит информацию о бронированиях.
- Поля:
    - `ID_booking`: (INT) Уникальный идентификатор бронирования, который служит первичным ключом.
    - `ID_room`: (INT) Идентификатор номера, который забронирован. Это поле используется как внешний ключ, ссылающийся на `ID_room` в таблице `Room`, что обеспечивает связь между бронированиями и номерами.
    - `ID_customer`: (INT) Идентификатор клиента, который сделал бронирование. Это поле используется как внешний ключ, ссылающийся на `ID_customer` в таблице `Customer`, которым мы обеспечиваем связь между бронированиями и клиентами.
    - `check_in_date`: (DATE) Дата заезда, указывающая, когда клиент планирует заехать в номер. Это обязательное поле.
    - `check_out_date`: (DATE) Дата выезда, указывающая, когда клиент планирует покинуть номер. Это обязательное поле.

#### Взаимосвязи
- Таблица `Room` ссылается на таблицу `Hotel`, обеспечивая связь между номерами и соответствующими гостиницами.
- Таблица `Booking` связывает номера и клиентов, обеспечивая информацию о том, какие номера были забронированы конкретными клиентами.
- Использование внешних ключей (в `Room` и `Booking`) поддерживает целостность данных, гарантируя, что все ссылки на гостиницы, номера и клиентов верны.

Данная структура базы данных эффективно организует и систематизирует информацию о гостиницах, номерах, клиентах и их бронированиях. Это позволяет удобно управлять данными, обеспечивая целостность информации и легкость доступа к различным аспектам гостиничного сервиса.

### Подготовительный этап:
1. Создадим БД hotels_booking в графическом интерфейсе.
2. Создадим таблицы, запустив скрипт из файла databases/hotels_booking/V1__create_tables.sql.
3. Наполним таблицы данными с помощью скрипта databases/hotels_booking/V2__insert_data.sql.

### Задачи:
#### Задача 1.
Условие:
Определить, какие клиенты сделали более двух бронирований в разных отелях,
и вывести информацию о каждом таком клиенте, включая его имя, электронную почту,
телефон, общее количество бронирований, а также список отелей, в которых
они бронировали номера (объединенные в одно поле через запятую с помощью CONCAT).
Также подсчитать среднюю длительность их пребывания (в днях) по всем бронированиям.
Отсортировать результаты по количеству бронирований в порядке убывания.

Решение:
размещено в скрипте databases/hotels_booking/V3__task1.sql.

#### Задача 2.
Условие:
Необходимо провести анализ клиентов, которые сделали более двух бронирований в разных
отелях и потратили более 500 долларов на свои бронирования.
Для этого:
Определить клиентов, которые сделали более двух бронирований и забронировали
номера в более чем одном отеле. Вывести для каждого такого клиента следующие данные:
ID_customer, имя, общее количество бронирований, общее количество уникальных отелей,
в которых они бронировали номера, и общую сумму, потраченную на бронирования.
Также определить клиентов, которые потратили более 500 долларов на бронирования,
и вывести для них ID_customer, имя, общую сумму, потраченную на бронирования,
и общее количество бронирований.
В результате объединить данные из первых двух пунктов, чтобы получить список клиентов,
которые соответствуют условиям обоих запросов. Отобразить поля: ID_customer, имя,
общее количество бронирований, общую сумму, потраченную на бронирования,
и общее количество уникальных отелей.
Результаты отсортировать по общей сумме, потраченной клиентами, в порядке убывания.

Решение:
размещено в скрипте databases/hotels_booking/V4__task2.sql.

#### Задача 3.
Условие:
Вам необходимо провести анализ данных о бронированиях в отелях и определить предпочтения
клиентов по типу отелей. Для этого выполните следующие шаги:

Категоризация отелей.
Определите категорию каждого отеля на основе средней стоимости номера:

«Дешевый»: средняя стоимость менее 175 долларов.
«Средний»: средняя стоимость от 175 до 300 долларов.
«Дорогой»: средняя стоимость более 300 долларов.
Анализ предпочтений клиентов.
Для каждого клиента определите предпочитаемый тип отеля на основе количества отелей в
каждой категории, которые они посетили.
Если у клиента одинаковое количество отелей в нескольких категориях,
выбирайте самую дорогую категорию:

Если у клиента есть хотя бы один «дорогой» отель, присвойте ему категорию «дорогой».
Если у клиента нет «дорогих» отелей, но есть хотя бы один «средний»,
присвойте ему категорию «средний».
Если у клиента нет «дорогих» и «средних» отелей, но есть «дешевые»,
присвойте ему категорию предпочитаемых отелей «дешевый».
Вывод информации.
Выведите для каждого клиента следующую информацию:

ID_customer: уникальный идентификатор клиента.
name: имя клиента.
preferred_hotel_type: предпочитаемый тип отеля.
visited_hotels: список уникальных отелей, которые посетил клиент.
Сортировка результатов.
Отсортируйте клиентов так, чтобы сначала шли клиенты с «дешевыми» отелями,
затем со «средними» и в конце — с «дорогими».

Решение:
размещено в скрипте databases/hotels_booking/V5__task3.sql.

## База данных 4. Структура организации.

### Условие.
Структура базы данных предназначена для управления информацией о сотрудниках, их ролях, департаментах, проектах и задачах. Она состоит из пяти таблиц: `Departments`, `Roles`, `Employees`, `Projects` и `Tasks`. Рассмотрим каждую таблицу подробнее.

#### 1. Таблица `Departments`
- Цель: Хранит информацию о департаментах в организации.
- Поля:
    - `DepartmentID`: (INT) Уникальный идентификатор департамента, который является первичным ключом. Этот идентификатор должен быть уникальным для каждой записи.
    - `DepartmentName`: (VARCHAR) Название департамента. Это обязательное поле (NOT NULL), которое не может быть пустым.

#### 2. Таблица `Roles`
- Цель: Хранит информацию о ролях сотрудников внутри организации.
- Поля:
    - `RoleID`: (INT) Уникальный идентификатор роли, который служит первичным ключом. Этот идентификатор должен быть уникальным.
    - `RoleName`: (VARCHAR) Название роли. Это также обязательное поле (NOT NULL), не допускающее пустых значений.

#### 3. Таблица `Employees`
- Цель: Хранит информацию о сотрудниках организации.
- Поля:
    - `EmployeeID`: (INT) Уникальный идентификатор сотрудника, который является первичным ключом. Этот идентификатор должен быть уникальным для каждого сотрудника.
    - `Name`: (VARCHAR) Имя сотрудника. Это обязательное поле (NOT NULL), которое не может быть пустым.
    - `Position`: (VARCHAR) Должность сотрудника. Это поле может быть пустым.
    - `ManagerID`: (INT) Идентификатор менеджера, который также является сотрудником. Это поле используется как внешний ключ, ссылающийся на `EmployeeID` в той же таблице `Employees`, что позволяет создать иерархию менеджеров и подчиненных.
    - `DepartmentID`: (INT) Идентификатор департамента, к которому принадлежит сотрудник. Это поле используется как внешний ключ, ссылающийся на `DepartmentID` в таблице `Departments`.
    - `RoleID`: (INT) Идентификатор роли, которая соответствует сотруднику. Это поле используется как внешний ключ, ссылающийся на `RoleID` в таблице `Roles`.

#### 4. Таблица `Projects`
- Цель: Хранит информацию о проектах организованными отделами.
- Поля:
    - `ProjectID`: (INT) Уникальный идентификатор проекта, который является первичным ключом. Этот идентификатор должен быть уникальным для каждого проекта.
    - `ProjectName`: (VARCHAR) Название проекта. Это обязательное поле (NOT NULL), не допускающее пустых значений.
    - `StartDate`: (DATE) Дата начала проекта. Это поле может быть пустым.
    - `EndDate`: (DATE) Дата окончания проекта. Это поле может быть пустым.
    - `DepartmentID`: (INT) Идентификатор департамента, который отвечает за проект. Это поле используется как внешний ключ, ссылающийся на `DepartmentID` в таблице `Departments`.

#### 5. Таблица `Tasks`
- Цель: Хранит информацию о задачах, назначенных на сотрудников в рамках проектов.
- Поля:
    - `TaskID`: (INT) Уникальный идентификатор задачи, который служит первичным ключом. Этот идентификатор должен быть уникальным для каждой задачи.
    - `TaskName`: (VARCHAR) Название задачи. Это обязательное поле (NOT NULL), не допускающее пустых значений.
    - `AssignedTo`: (INT) Идентификатор сотрудника, которому назначена задача. Это поле используется как внешний ключ, ссылающийся на `EmployeeID` в таблице `Employees`.
    - `ProjectID`: (INT) Идентификатор проекта, к которому относится задача. Это поле используется как внешний ключ, ссылающийся на `ProjectID` в таблице `Projects`.

#### Взаимосвязи
- Таблицы `Employees`, `Projects`, и `Tasks` связаны между собой через внешние ключи, что позволяет интегрировать данные о сотрудниках, их задачах и проектах.
- `ManagerID` в `Employees` позволяет создать иерархическую структуру управления, связывая сотрудников с их менеджерами.
- `DepartmentID` связывает `Employees` с соответствующими департаментами, а также проекты с организацией в рамках определенного департамента.
- `RoleID` связывает сотрудников с их ролями, что позволяет классифицировать их функции внутри компании.

Данная структура базы данных обеспечивает четкое управление данными о департаментах, ролях сотрудников, их проектах и задачах. Это позволяет эффективно организовывать, отслеживать и управлять ресурсами и задачами в компании, что является ключевым для успешного функционирования и достижения бизнес-целей.

### Подготовительный этап:
1. Создадим БД company_structure в графическом интерфейсе.
2. Создадим таблицы, запустив скрипт из файла databases/company_structure/V1__create_tables.sql.
3. Наполним таблицы данными с помощью скрипта databases/company_structure/V2__insert_data.sql.

#### Задачи:
#### Задача 1.
Условие:
Найти всех сотрудников, подчиняющихся Ивану Иванову (с EmployeeID = 1),
включая их подчиненных и подчиненных подчиненных. Для каждого сотрудника вывести следующую информацию:

EmployeeID: идентификатор сотрудника.
Имя сотрудника.
ManagerID: Идентификатор менеджера.
Название отдела, к которому он принадлежит.
Название роли, которую он занимает.
Название проектов, к которым он относится (если есть, конкатенированные в одном столбце через запятую).
Название задач, назначенных этому сотруднику (если есть, конкатенированные в одном столбце через запятую).
Если у сотрудника нет назначенных проектов или задач, отобразить NULL.
Требования:
Рекурсивно извлечь всех подчиненных сотрудников Ивана Иванова и их подчиненных.
Для каждого сотрудника отобразить информацию из всех таблиц.
Результаты должны быть отсортированы по имени сотрудника.
Решение задачи должно представлять из себя один sql-запрос и задействовать ключевое слово RECURSIVE.

Решение:
размещено в скрипте databases/company_structure/V3__task1.sql.

#### Задача 2.
Условие:
Найти всех сотрудников, подчиняющихся Ивану Иванову с EmployeeID = 1,
включая их подчиненных и подчиненных подчиненных. Для каждого сотрудника вывести следующую информацию:

EmployeeID: идентификатор сотрудника.
Имя сотрудника.
Идентификатор менеджера.
Название отдела, к которому он принадлежит.
Название роли, которую он занимает.
Название проектов, к которым он относится (если есть, конкатенированные в одном столбце).
Название задач, назначенных этому сотруднику (если есть, конкатенированные в одном столбце).
Общее количество задач, назначенных этому сотруднику.
Общее количество подчиненных у каждого сотрудника (не включая подчиненных их подчиненных).
Если у сотрудника нет назначенных проектов или задач, отобразить NULL.

Решение:
размещено в скрипте databases/company_structure/V4__task2.sql.

#### Задача 3.
Условие:
Найти всех сотрудников, которые занимают роль менеджера и имеют подчиненных
(то есть число подчиненных больше 0). Для каждого такого сотрудника вывести следующую информацию:

EmployeeID: идентификатор сотрудника.
Имя сотрудника.
Идентификатор менеджера.
Название отдела, к которому он принадлежит.
Название роли, которую он занимает.
Название проектов, к которым он относится (если есть, конкатенированные в одном столбце).
Название задач, назначенных этому сотруднику (если есть, конкатенированные в одном столбце).
Общее количество подчиненных у каждого сотрудника (включая их подчиненных).
Если у сотрудника нет назначенных проектов или задач, отобразить NULL.

Решение:
размещено в скрипте databases/company_structure/V5__task3.sql.w