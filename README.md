<div align="center">

# Teivrim

**Rust · C++ · Unreal Engine · C**

Нейронаука и ML · геймплей · движки и редакторы · системное программирование

[![CI](https://github.com/Teivrim/ImGui-Editor-Starter/actions/workflows/ci.yml/badge.svg)](https://github.com/Teivrim/ImGui-Editor-Starter/actions/workflows/ci.yml)
[![услуги](https://img.shields.io/badge/услуги-teivrim.github.io-5eead4?style=for-the-badge)](https://teivrim.github.io)
[![Telegram](https://img.shields.io/badge/Telegram-@TEIVRIM-2AABEE?style=for-the-badge)](https://t.me/TEIVRIM)
[![CI](https://github.com/Teivrim/rust-course/actions/workflows/ci.yml/badge.svg)](https://github.com/Teivrim/rust-course/actions/workflows/ci.yml)
[![CI](https://github.com/Teivrim/PolygonEditor/actions/workflows/ci.yml/badge.svg)](https://github.com/Teivrim/PolygonEditor/actions/workflows/ci.yml)
[![CI](https://github.com/Teivrim/TDEvuris/actions/workflows/ci.yml/badge.svg)](https://github.com/Teivrim/TDEvuris/actions/workflows/ci.yml)

</div>

---

## Проекты

### [FlyTest](https://github.com/Teivrim/FlyTest) — нейронаука + ML

Локальный цифровой цирк для виртуальной мухи. Замкнутый контур
`мир → Observation → Brain → Action → Blender`, Rust-runtime и
`TFLY.h` — single-header C-библиотека на 106 КБ со всей моделью:
сенсоры, боль, гормоны, эмоции, потребности, память, обучение, сон.

Два решения, ради которых стоит открыть:

```toml
[lints.rust]
unsafe_code = "deny"     # unsafe запрещён на уровне крейта
```

FFI-модуль локально делает `#[allow(unsafe_code)]`, всё остальное — нет.
Мост в C не расползается на пол-проекта. И `build.rs` не роняет сборку,
если компилятора нет: крейт собирается, `crate::tfly` сообщает, что
фича недоступна.

Плюс анализ графа связей FlyWire FAFB v783 через SQLite, JSONL-протокол
для внешних моделей, адаптеры под PyTorch/ONNX/spiking/RL.

### [UE-Gameplay-Kit](https://github.com/Teivrim/UE-Gameplay-Kit) — геймплей на UE 5.8

Три раздельных `GameMode` в одном проекте: Combat, SideScrolling,
Platforming. 5 192 строки в 87 файлах, 29 типов `UCLASS`/`USTRUCT`/`UENUM`,
ноль сторонних зависимостей.

Логику поведения видно с двух сторон и это не дань моде: решения принимает
StateTree, а задачи и условия — C++-классы (`CombatStateTreeUtility`,
`SideScrollingStateTreeUtility`). Их можно править в редакторе, не пересобирая
модуль. EQS-контексты цели и опасности — отдельные `UEnvQueryContext`, а не
лямбды в GameMode, поэтому их переиспользуют в любом дереве запросов.

**Движок в CI не собирается** — UE 5.8 это около 100 ГБ, и лицензия не
разрешает ставить его на hosted runner. Вместо того чтобы объявить проверку
невозможной, `scripts/check_uproject.py` ловит то, что видно из исходников и
из-за чего проект не собирается: `UCLASS` без `.generated.h` или с ним не
последним, модуль без строки в `Build.cs`, выключенный плагин, заголовок,
который никто не включает. Он нашёл одну настоящую ошибку:
`UPhysicsConstraintComponent` в `CombatDummy` без модуля `PhysicsCore`.

Что проверка не ловит, написано у неё в выводе: существование заголовков
движка. Без установленного UE нельзя отличить сломанный include от include
движка, и первая версия проверки именно этим и обзавелась — 236 расхождений,
из которых полезных ноль.

### [YandexGame](https://github.com/Teivrim/YandexGame) — 4 игры в сторе

Браузерные игры на чистых HTML/CSS/JS с Canvas 2D, **все опубликованы**:
[NEON//COURIER](https://teivrim.itch.io/neon-courier) (аркада на выживание),
NEON//BASTION (башенная оборона, 30 волн), NEON//DESCENT (roguelite, 10 этажей,
3 класса), NEON//VECTOR (точная платформенная аркада, рекорды времени).
У одной из них адаптер официального Yandex Games SDK.

Здесь важно другое: это не «проект в репозитории», это **законченные
продукты, дошедшие до пользователя**. Релизный цикл, ассеты для листингов,
публикация.

### [ImGui-Editor-Starter](https://github.com/Teivrim/ImGui-Editor-Starter) — каркас редактора

C++17, Dear ImGui + OpenGL: документ, слои, композиция, undo/redo, менеджер
плагинов, планировщик задач, цепочка эффектов. 4 782 строки в 24 файлах,
подсистемы разделены по каталогам.

**Собирается офлайн одной командой.** GLFW, Dear ImGui, stb и GLAD 2
вендорёны в `third_party` — 61 МБ исходников в репозитории, `FetchContent`
нет вообще. CI падает, если зависимости вернутся в сеть или если вернётся
GLEW: обе поломки молчаливые до чистой машины, и на них проект и стоял.

### [rust-course](https://github.com/Teivrim/rust-course) — Rust с нуля

20 модулей, **14 912 строк, ноль зависимостей**. Только `std` — ни `serde`,
ни `glam`, ни `anyhow`. Каждый модуль — отдельный бинарник, поэтому ошибка
в модуле 7 не блокирует модуль 8. Харнесс ловит `todo!()` через
`catch_unwind` и ставит оценку. `cargo build --release` → 20 бинарников
за 15 секунд, сети не нужно вообще.

### [PolygonEditor](https://github.com/Teivrim/PolygonEditor) — 3D-редактор

C++17 / OpenGL, импорт FBX через Assimp, два рендер-бэкенда, CMake.
Зависимости вендорёны — собирается **без сети** на любой машине.

### [NovellEngine](https://github.com/Teivrim/NovellEngine) — редактор новел

C++20 / Win32: таймлайн, инспектор, undo/redo на уровне команд, формат
`.vne`. **3 319 строк, ноль сторонних библиотек.** Рендер вынесен за
абстракцию, чтобы позже можно было подключить D2D, не трогая панели.

### [TDEvuris](https://github.com/Teivrim/TDEvuris) — сканеры Windows

13 отдельных бинарников вместо монолита: так упавший детектор не роняет
остальные, и можно собрать конвейер из нужного. Подписи и эвристики как
два независимых механизма детекции. Чистый Win32, без зависимостей.

| | строк | зависим. |
|---|---:|---:|
| rust-course | 14 912 | **0** |
| PolygonEditor | 3 801 | 4 |
| NovellEngine | 3 319 | **0** |
| TDEvuris | 3 253 | **0** |

---

## Сборка проверяется в CI

Каждый репозиторий с workflow: при каждом коммите GitHub собирает проект
на свежем раннере. Это не обещание в README, это проверяемый факт.

| Репозиторий | Что делает CI |
|---|---|
| [rust-course](https://github.com/Teivrim/rust-course) | собирает 20 бинарников, гоняет 19 модулей, clippy |
| [PolygonEditor](https://github.com/Teivrim/PolygonEditor) | CMake + Ninja, MinGW, проверка бинарника |
| [TDEvuris](https://github.com/Teivrim/TDEvuris) | CMake + MSVC, проверка бинарника |
| [NovellEngine](https://github.com/Teivrim/NovellEngine) | `build.bat`, MinGW g++ |
| [FlyTest](https://github.com/Teivrim/FlyTest) | C-ядро TFLY + Rust-runtime, MinGW |
| [YandexGame](https://github.com/Teivrim/YandexGame) | синтаксис JS, состав поставки |
| [ImGui-Editor-Starter](https://github.com/Teivrim/ImGui-Editor-Starter) | CMake + Ninja, офлайн-сборка, запрет возврата GLEW |
| [UE-Gameplay-Kit](https://github.com/Teivrim/UE-Gameplay-Kit) | согласованность UE-проекта без движка, наличие ассетов |

**Что этот CI уже нашёл.** Репозиторий проходил локальную сборку, но не
собирался на чистой машине. Причины оказались неочевидными:

- `.gitignore` вырезал `src/bin/` вместе со сборкой — все 20 модулей курса
  отсутствовали в репозитории, хотя лежали на диске;
- макросы `min`/`max` из `<windows.h>` ломали `std::min` под MSVC (`C2589`);
- код использовал designated initializers при `CMAKE_CXX_STANDARD 17` —
  MinGW прощал как расширение, MSVC отказывался (`C7555`);
- точка входа была `WinMain`, а линковка шла как `/subsystem:console`;
- в `rustup set profile minimal` не входят `rustfmt` и `clippy`, поэтому
  `cargo fmt` и `cargo clippy` падали с подсказкой «run `rustup component
  add`». Код был чистым всё это время, а падали две проверки из одиннадцати;
- `FetchContent` тянул GLFW, Dear ImGui и stb из сети, хотя все три уже
  лежали в `third_party` — проект не собирался без интернета, хотя всё
  нужное было рядом;
- `GLEW` в теге `glew-2.2.0` содержит только шаблон `glew.c.in`, а
  настоящий `glew.c` генерируется шагом, который CMake не выполняет;
- `PhysicsCore` не был объявлен в `Build.cs`, хотя `CombatDummy` создаёт
  `UPhysicsConstraintComponent`.

Локальная сборка этого не показывала: машина была одна и всегда одна и та же.
Клонировать репозиторий на чужой компьютер — единственный честный тест,
и CI делает его бесплатно на каждом коммите.

Три из этих пяти поломок жили не в коде, а в обвязке: `.gitignore`,
профиль `rustup`, шаблон `CMakeLists`. Их не видно ни при каком чтении
исходников — видно только на чистой машине.

---

## Услуги

| Что делаю | От |
|---|---|
| Геймплей на C++ под UE5: StateTree, EQS, AI-контроллеры, core-системы | 25 000 ₽ |
| Инструменты и редакторы на C++/OpenGL под проект | 40 000 ₽ |
| Профилирование и починка производительности | 15 000 ₽ |
| Обучение C++-разработчиков Rust | 20 000 ₽ |
| Разбор и перенос легаси-кода | 12 000 ₽ |

Подробнее: **[teivrim.github.io](https://teivrim.github.io)**

---

## Как работаю

- **Сначала критерии приёмки.** Если задача звучит как «сделай, чтобы работало» — говорю сразу, а не после.
- **Не беру задачу, если не влезает в бюджет.** Предлагаю, что урезать. Не делаю наполовину.
- **Отдаю то, что собирается.** Сборка одной командой у заказчика, а не «у меня работает».
- **Показываю провалы тоже.** В репозиториях лежит `BUILD-REPORT.md` с настоящим результатом сборки — включая то, что не собралось и почему.

---

<div align="center">

**[Написать в Telegram](https://t.me/TEIVRIM)** · [услуги и портфолио](https://teivrim.github.io)

</div>
