Tabix is open source simple BI and sql editor tool for Clickhouse. 
==================================================================


Tabix - это инструмент для создания запросов к базе данных - ClickHouse



## Install and run


Для старта ипользованая Tabix, нужно подкорректировать настройки Clickhouse. 

Нужно разрешить подключаться с вашего IP адресса к CH, добавив listen_host в `/etc/clickhouse-server/config.xml` 

```xml
<listen_host>111.222.111.222</listen_host>
```


Далее заходим на `ui.tabix.io`


![Alt Text](articel01img/tabixlogin.png)

Заполняем:
* В поле url ваш адресс к серверу СH `http://clickhouse.ip:8123`
* Login & Password
* Другие парамерты оставдяем пустми




Основной экран Tabix
==================================================================
![tabixmainpage](articel01img/tabixmainpage2.png)



В левой части расположенно дерево обьектов

В центральной части SQL редактор,

В нижней части результат

Основной экран Tabix - Дерево
==================================================================


В левой часте расположенны все базы данных узла к которому вы подключены.

На каждой таблице можно кликнуть правой кнопкой и получить дополнительне действия над таблицей.


![Tabix MultiQuery Chart](articel01img/treeRightClick.png)



Развернув таблицу можно получить список полей, кликая мышкой - поле будет автоматически вставляться в SQL редактор.

Кнопка `Reload structure` необходим для обновления стурктуры базы, т/к дерево обьектов кэшируется

Можно открыть для просмотра таблицу сделав DoubleClick

![Tabix MultiQuery Chart](articel01img/TablePreview.png)


Так же в дереве:
Display the number of tables at the database
The icon of the table depends on its engine



Основной экран Tabix - Редактор
==================================================================

## Auto complete

Как работает автокомплит


## Multiquery in editor

Todo: - Как использовать `;;`


![Tabix MultiQuery Chart](articel01img/MultiQuery.png)



## Editor right click menu

![Tabix Editor rightmenu](articel01img/EditorRightMenu.png)


## Tabix HotKeys

Какие горячие клавиши есть в редакторе

| Windows/Linux                  | Mac                            | Action                         |
|:-------------------------------|:-------------------------------|:-------------------------------|
| Ctrl-Enter | Command-Enter | Exec current query under cursor |
| Shift-Ctrl-Enter | Shift-Command-Enter | Exec all query in current editor |
| Ctrl-Shift-F | Command-Shift-F | AutoFormat code |
| Alt-Shift-Ctrl-Left | Command-Alt-Shift-Right | Goto Next tab |
| Alt-Shift-Ctrl-Right | Command-Alt-Shift-Right | Goto Prev tab  |
| Shift-Ctrl-[0...9] | Command-Shift-[0...9] | Goto tab number |
| Shift-Ctrl-+ | Command-Shift-+ | Fold code |
| Shift-Ctrl-- | Command-Shift-- | Unfold code |
| Alt-L, Ctrl-F1 | Command-Option-L, Command-F1 | Fold selection |
| Alt-Shift-L, Ctrl-Shift-F1 | Command-Option-Shift-L, Command-Shift-F1 | Unfold |
| Alt-0 | Command-Option-0 | Fold all |
| Alt-Shift-0 | Command-Option-Shift-0 | Unfold all |

### Line Operations

| Windows/Linux                  | Mac                            | Action                         |
|:-------------------------------|:-------------------------------|:-------------------------------|
| Ctrl-D | Command-D | Remove line |
| Ctrl-Y | Command-Y | Remove line |
| Alt-Shift-Down | Command-Option-Down | Copy lines down |
| Alt-Shift-Up | Command-Option-Up | Copy lines up |
| Alt-Down | Option-Down | Move lines down |
| Alt-Up | Option-Up | Move lines up |
| Alt-Delete | Ctrl-K | Remove to line end |
| Alt-Backspace | Command-Backspace | Remove to linestart |
| Ctrl-Backspace | Option-Backspace, Ctrl-Option-Backspace | Remove word left |
| Ctrl-Delete | Option-Delete | Remove word right |


### Find/Replace

| Windows/Linux                  | Mac                            | Action                         |
|:-------------------------------|:-------------------------------|:-------------------------------|
| Ctrl-F | Command-F | Find |
| Ctrl-H | Command-Option-F | Replace |
| Ctrl-K | Command-G | Find next |
| Ctrl-Shift-K | Command-Shift-G | Find previous |


### Other

| Windows/Linux                  | Mac                            | Action                         |
|:-------------------------------|:-------------------------------|:-------------------------------|
| Ctrl-Shift-U | Ctrl-Shift-U | Change to lower case |
| Ctrl-U | Ctrl-U | Change to upper case |
| Ctrl-/ | Command-/ | Toggle comment |
| Ctrl-Shift-D | Command-Shift-D | Duplicate selection |


More hot keys  https://github.com/ajaxorg/ace/wiki/Default-Keyboard-Shortcuts#line-operations



Todo: - Зачем переключатель Базы


Minimizes brackets and subqueries

The list of functions is loaded based on the capabilities of the server




Основной экран Tabix - Результаты запросов - Таблицы
==================================================================

Todo: - выгрузка в эксель / redmine /

![Tabix Redmine export](articel01img/redmine_export.png)


Redmine format data:
```
 | Carrier | DestCityName |
 | EV | Chicago, IL |
 | DL | Minneapolis, MN |
 | WN | Dallas, TX |
 | WN | Chicago, IL |
 | B6 | Boston, MA |
 | EV | Atlanta, GA |
 | AA | Philadelphia, PA |
```



Todo: - Трансформация / переворот таблицы

![Tabix Transpose Table](articel01img/TransposeTable.png)

Todo: - стилизация ячеек и форматирования

![Tabix Style cell](articel01img/StylingCelss.png)

Todo: - расчет median / avg по выделенным ячейкам

![Tabix Calc avg](articel01img/CalcAVG.png)



Основной экран Tabix - Результаты запросов - Графики
==================================================================

Воспользуемся DataSet OnTime:  https://clickhouse.yandex/docs/ru/single/index.html#ontime




Выполним простой запрос, где в результате выполнения первое поле в формате `Date`

```sql


SELECT
 FlightDate, count() as fly
FROM
  ontime
GROUP BY FlightDate
```

Если сразу перейти на вкладку "Draw"

![Tabix DRAW Chart](articel01img/fly.png)

Выполним другой запрос:

```sql
SELECT
 Carrier ,count() as fly
FROM
  ontime
GROUP BY Carrier
HAVING fly>1000

```
![Tabix GROUP BY draw chart](articel01img/GROUPBYCarrier.png)

```sql
SELECT
 FlightDate, Carrier ,count() as fly
FROM
  ontime
GROUP BY FlightDate,Carrier
HAVING fly>1000
```
![Tabix GROUP BY DATE chart](articel01img/FlightDate,Carrier.png)







Пару примеров как строить сложные графики

*DRAW_SANKEYS*

https://tabix.io/doc/draw/Draw_Sankeys/


```sql
SELECT
 Carrier , DestCityName ,count() as fly
FROM
  ontime
GROUP BY Carrier,DestCityName
HAVING fly>5000
DRAW_SANKEYS  "Carrier.fly.DestCityName"
```

![Tabix SANKEYS](articel01img/DRAW_SANKEYS_Carrier.fly.DestCityName.png)



*DRAW_TREEMAP*

https://tabix.io/doc/draw/Draw_Treemap/



```sql
SELECT
 Carrier , DestCityName ,count() as fly
FROM
  ontime
GROUP BY Carrier,DestCityName
HAVING fly>1000
DRAW_TREEMAP  "Carrier.DestCityName"
```
![Tabix TREEMAP](articel01img/DRAW_TREEMAP_Carrier.DestCityName.fly.png)


*DRAW_CALENDAR*

```sql

SELECT
 FlightDate, count() as fly
FROM
  ontime
GROUP BY FlightDate
DRAW_CALENDAR {}
```
![Tabix CALENDAR](articel01img/DRAW_CALENDAR.png)
