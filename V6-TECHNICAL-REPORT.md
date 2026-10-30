# V6 — технический отчёт

Объект: установленный **Cutive Mono Cyrillic 6.020** в Arch Linux.
Дата проверки: 2026-10-30. Все проверки — только чтение; шрифт, исходники,
Fontconfig, fallback и системная установка не изменялись.

## 1. Точная идентификация

| Параметр | Значение |
|---|---|
| Путь установленного файла | `/home/sora/.local/share/fonts/CutiveMonoCyrillic/CutiveMono-Cyrillic-Regular.ttf` |
| Формат | TrueType (TTF, sfnt; таблица `glyf`) |
| Семейство | `Cutive Mono Cyrillic` |
| Стиль | `Regular` |
| Full name | `Cutive Mono Cyrillic Regular` |
| PostScript name | `CutiveMonoCyrillic-Regular` |
| Version string | `Version 6.020; ttfautohint (v1.8.4.16-eb64)` |
| Font Revision | `6.020004` (float-представление; name ID 5 — 6.020) |
| UPM | 2048 |
| ascent / descent / lineGap | 1697 / −558 / 0 |
| Глифы | 582 |
| cmap | 577 |
| SHA-256 | `aaf8154e9983c661e88c4a3769266d2c4c1f3ff55a2cc063c5f1f397faac55f7` |
| Размер | 129 852 B |
| head.created | 2012-09-19 19:30:31 |
| head.modified | 2026-10-30 12:40:16 UTC (локально ~15:40) |
| mtime установленного файла | 2026-10-30 15:41:27 +03:00 |

Установленный файл побайтово совпадает с проектной сборкой
`CutiveMono-Cyrillic-Regular.ttf`: SHA-256 одинаковый. Копия для аудита —
`fonts/installed-v6.ttf`, SHA-256 тот же. Оригинал —
`fonts/original-cutive-mono.ttf`, SHA-256
`96a36a00079058684982f61ee334323f8b501d7b68dcecd6049a4f9177e3a62c`.

Large-семейство: `Cutive Mono Cyrillic Large 6.020`, SHA-256
`620a90ea7fa2d037a12341d65e46d811b8cf75ddd57008969423d6ab5910e730`.
Оно не является предметом основного разбора; `verify.py` для него проходит.

## 2. Состав и покрытие

| Категория | Количество |
|---|---|
| Всего глифов | 582 |
| Латиница донора | **452** |
| Кириллица U+0400–U+04FF | **128** |
| Русский алфавит | 33 заглавных + 33 строчных |
| Украинские | 8 (`Ґґ Єє Іі Її`) |
| Белорусские | 2 (`Ўў`) |
| Сербские / македонские | 22 (`Ѐѐ Ѝѝ Јј Ѕѕ Ѓѓ Ќќ Љљ Њњ Џџ Ђђ Ћћ`) |
| Расширенная кириллица | 30 (`Ҷҷ Ӂӂ Ӑӑ Ӓӓ Ӗӗ Ӝӝ Ӟӟ Ӣӣ Ӥӥ Ӧӧ Ӯӯ Ӱӱ Ӳӳ Ӵӵ Ӹӹ`) |
| Комбинируемые знаки | 16 (U+0300–U+0328, advance 0) |
| Пунктуация | № U+2116, ₽ U+20BD |

cmap: две субтаблицы format 4 (platform 0/encoding 3 и platform 3/encoding 1),
по 577 записей, словари совпадают. Дубликатов Unicode и multi-mapped глифов
нет. Все кодпоинты лежат в BMP; format 12 не требуется.

## 3. Метрики и моноширинность

| Advance | Глифов | Комментарий |
|---|---|---|
| 1240 | 560 | все буквы, цифры, пунктуация |
| 0 | 16 | комбинируемые знаки |
| 165 | 1 | `periodcentered` U+00B7 — исходное исключение донора |

Других значений нет. Все кириллические буквы — 1240; шрифт моноширинный.
Вертикальные метрики: 1697 / −558, UPM 2048.

Измеренная толщина (растр 2048 px/em, 1 px = 1 unit): Latin `l`/`i` — 96;
`п`/`н`/`ш` — 96; `Ц`/`ц` — 96; `ь` — 93–94; `ы` второй стем — 96;
`Ц` нижняя планка — 86; `ц` — 82; засечки — 86. Это соответствует весу V6
(стемы 96, горизонтали 86/82). В 6.020 относительно 6.010 изменены только
`afii10040` (Ц) и `afii10088` (ц); остальные контуры бит-в-бит те же.

## 4. Латиница

* 452/452 оригинальных глифов присутствуют;
* 0 изменённых контуров: совпадают координаты, флаги, `endPtsOfContours`,
  компоненты;
* Latin cmap донора — 447 записей; латинские записи не переписаны.

Это проверено `verify.py` и независимым сравнением `glyf`.

## 5. Unicode, NFC/NFD

* NFC/NFD: проверено 28 пар; 28/28 дают одинаковый результат.
* Для пар с прекомпозом HarfBuzz собирает базу+знак в готовый глиф через
  `ccmp`; для пар без прекомпоза работает GPOS.
* Примеры GPOS-фолбэка:
  * `а` + U+0301 → `afii10065` + `acutecomb`, смещение (−1306, −45);
  * `щ` + U+0301 → `afii10091` + `acutecomb`;
  * `с` + U+0327 → `afii10083` + `uni0327`, смещение (−724, −53).
* Маркеры имеют advance 0 и позиционируются над/под базой.

## 6. GSUB/GPOS

| Таблица | Features | Lookups |
|---|---|---|
| GSUB | `aalt case ccmp frac liga locl ordn sups` | 16 |
| GPOS | `kern mark mkmk` | 7 |

Проверки шейпинга: `fi`/`fl` → лигатуры; `1/2` + `frac` → `onehalf`;
`1o` + `ordn` → `ordmasculine`; `liga` выключается; `mark`/`mkmk`
присутствуют. `kern` есть, но в моноширинном наборе advance не меняется.

## 7. Fontconfig

```
$ fc-match "Cutive Mono Cyrillic"
CutiveMono-Cyrillic-Regular.ttf: "Cutive Mono Cyrillic" "Regular"

$ fc-scan --format '%{family}\t%{style}\t%{fontversion}\n' \
    /home/sora/.local/share/fonts/CutiveMonoCyrillic/CutiveMono-Cyrillic-Regular.ttf
Cutive Mono Cyrillic	Regular	394527
```

Цепочка `fc-match -s "Cutive Mono Cyrillic"` начинается с установленного
файла, далее Noto Sans Mono, DejaVu Sans Mono, Noto Sans Mono CJK KR,
Iosevka Nerd Font. Fontconfig и fallback не изменялись.

## 8. Nerd Fonts fallback

В самом шрифте нет PUA/Nerd-иконок (проверено по cmap: PUA-кодпоинтов нет).
В системе установлены JetBrainsMono Nerd Font, Iosevka Nerd Font и другие;
`fc-match -s` включает Iosevka Nerd Font. В foot 14 px иконки `󰊢`/`󰣇`
отрисовались из системного fallback, а не из V6 — это ожидаемое поведение.
В kitty визуальная проверка иконок не подтверждена (см. раздел 9).

## 9. Реальные приложения

| Приложение | Кегль | Результат |
|---|---|---|
| **foot** | 14 px | Установленный V6 выбран через fontconfig; кириллица, латиница и Nerd-иконки отрисованы. Скриншот: `screenshots/10-foot.png`. |
| **kitty** | 14 px | Запуск был, но окно оказалось перекрыто полноэкранной игрой; валидный скриншот не получен. **Визуальная проверка kitty не подтверждена**, результат не имитируется. |

Размеры 11–24 px проверены в растровых образцах
`screenshots/07-small-size-11-12px.png`, `08-normal-size-13-14px.png`,
`09-large-size-16-20px.png` (FreeType/PIL, фактический растр + NEAREST-зум). Это не заменяет проверку
kitty, а показывает поведение хинтинга/растеризации в контролируемых условиях.

## 10. Целостность контуров и таблиц

* 128/128 кириллических глифов: нет пустых, нет отрицательного числа
  контуров, нет нефинитных bbox.
* `pathops.simplify` — 128/128.
* `audit.py`: `clean; 66 glyphs checked`; паразитных белых островков нет.
* Обнаружены **8 глифов / 9 сегментов** с повторяющимися подряд точками:
  U+0404, U+0409, U+0414, U+042A, U+044A, U+044C, U+044F (2), U+0491.
  В основном control point совпадает с on-curve; `pathops.simplify` проходит,
  растр чистый. Это косметический шум, не повреждение.
* TTF round-trip `fontTools` save → reload — OK.
* Проектный OTF round-trip — OK; OTF **не установлен**.
* `ots-sanitize` и `hb-shape` не установлены; использованы `fontTools`,
  `uharfbuzz`, `fc-scan`.

## 11. Обнаруженные технические проблемы

### 11.1. U+04B6/04B7 — неверная семантика

`Ҷ`/`ҷ` (Che with descender) собраны как **Zhe + breve** и совпадают с
`Ӂ`/`ӂ` (U+04C1/04C2): bbox `50…1190 × 0…1469` и `148…1093 × 0…1111`,
`yMin = 0`. У правильной Che with descender должен быть отрицательный `yMin`
и не должно быть breve. Это есть в V5, 6.010 и 6.020; в 6.020 не
исправлялось. Причина — `source/design/extras.py`, `COMPOSITES`:
`(0x04B6, "\u0416", "brevecomb")`, `(0x04B7, "\u0436", "brevecomb")`.
Визуально — `screenshots/11-extended-issue.png`.

### 11.2. Документация и фактические хвосты

`docs/V6-01.md` говорит о засечке 396×86 у хвоста Ц/Щ. Фактические контуры:
6.010 — 289/230 (строчные 260/190), 6.020 — 246/246. Это расхождение
документации и кода; на качество шрифта не влияет, но ревьюеру стоит знать.

### 11.3. Прочее

* `periodcentered` U+00B7 — 165 advance, исходное исключение донора.
* cmap только format 4; для текущего BMP-набора этого достаточно.
* `head.fontRevision` — float `6.020004`; name ID 5 — `6.020`.
* OTF не установлен; если он используется, нужна отдельная проверка.

## 12. Что не проверялось

* Художественное качество и уместность форм — только материал для ревью.
* Печать, PDF, все терминалы/браузеры/DPI.
* Полный ручной кернинг и оптические пары (advance фиксирован).
* Kitty — визуально не подтверждён (окно перекрыто игрой).
* Firefox/Safari и другие ОС.
* `ots-sanitize`, `hb-shape` — утилиты отсутствуют.

## 13. Воспроизводимость

```bash
cd /home/sora/Projects/Cutive-Mono-Cyrillic
sha256sum V6-REVIEW/fonts/*.ttf
fc-match "Cutive Mono Cyrillic"
fc-scan --format '%{family}\t%{style}\t%{fontversion}\n' \
  /home/sora/.local/share/fonts/CutiveMonoCyrillic/CutiveMono-Cyrillic-Regular.ttf
.venv/bin/python source/tools/verify.py V6-REVIEW/fonts/installed-v6.ttf
.venv/bin/python source/tools/audit.py
```

`verify.py`:

```
- Latin glyphs checked: 452, changed: 0
- advance width 1240 for 560 glyphs
- cmap entries: 577
- hinted Cyrillic glyphs: 128, unhinted: 0

OK: all checks passed
```

## 14. Итог

* Установленный V6 — **6.020**, `Cutive Mono Cyrillic`; файл побайтово
  совпадает с проектной сборкой.
* Латиница 452/452 не изменена; кириллица 128/128 присутствует и хинчена;
  advance 1240; GSUB/GPOS и лигатуры на месте.
* 6.020 отличается от 6.010 только Ц/ц.
* Технических блокеров для основной латиницы и русской кириллицы нет.
* Есть семантическая ошибка U+04B6/04B7 (Che with descender → Zhe+breve),
  косметические повторяющиеся точки и расхождение документации по хвостам.
