# osm-moscow

выбранный город - МОСКВА. заправки. openstreetmap. утилита строит выпуклую оболочку, ищет две самые близкие заправки и считает сколько их в районе кунцево. все числа и подробности в ДЗ5_Отчет_ИвашкинГС_М08-603ДИП.pdf. вывод всех команд в ДЗ5_ИвашкинГС_М08-603ДИП.txt

данные уже лежат в data/ - качать ничего не надо

## что делает каждая команда

- project - переводит широты и долготы в дециметры. пишет data/points.txt и data/district.txt
- hull - выпуклая оболочка. площадь и периметр
- closest - две самые близкие заправки. с --brute то же самое перебором
- inside - сколько заправок в кунцево и площадь кунцево
- plot - картинка plot.png
- check.py - сверка всего этого с библиотекой shapely

## мак

нужен питон 3.10 или новее.

качаем репо

```
git clone https://github.com/Schizzzx/osm-moscow
cd osm-moscow
```

ставим библиотеки в .venv

```
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
```

запускаем по порядку

```
.venv/bin/python geo.py project data/fuel.json data/kuntsevo.geojson
.venv/bin/python geo.py hull data/points.txt
.venv/bin/python geo.py closest data/points.txt
.venv/bin/python geo.py closest data/points.txt --brute
.venv/bin/python geo.py inside data/points.txt data/district.txt
.venv/bin/python geo.py plot data/points.txt data/district.txt plot.png
.venv/bin/python check.py data/points.txt data/district.txt
sh tests/run_tests.sh
```

перекачать данные заново - `sh get_data.sh` (нужен uv). но это не обязательно

## винда

1. качаем питон и устанавливаем его в PATH
2. качаем репо
3. открываем папку что мы только что клонировали в проводнике
4. в адресной строке проводника пишем cmd и жмем enter - откроется консоль сразу в этой папке

ставим библиотеки в .venv (один раз)

```
py -m venv .venv
.venv\Scripts\python -m pip install -r requirements.txt
```

если "py" не работает
попробуйте "python"

запускаем по порядку

```
.venv\Scripts\python geo.py project data/fuel.json data/kuntsevo.geojson
.venv\Scripts\python geo.py hull data/points.txt
.venv\Scripts\python geo.py closest data/points.txt
.venv\Scripts\python geo.py closest data/points.txt --brute
.venv\Scripts\python geo.py inside data/points.txt data/district.txt
.venv\Scripts\python geo.py plot data/points.txt data/district.txt plot.png
.venv\Scripts\python check.py data/points.txt data/district.txt
```

get_data.sh и tests/run_tests.sh на винде не запустятся - это скрипты для мака. они и не нужны

## если все ок

- hull - 15 вершин. площадь 1566 км2
- closest - 7.52 м. node/1397055963 и way/126726831
- inside - 6 внутри. 825 снаружи
- check.py - в конце "ИТОГ: все сошлось"
