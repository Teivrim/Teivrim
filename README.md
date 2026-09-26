<div align="center">

# Teivrim

**Программист C++ / Unreal Engine**

Геймплей · core-системы · AI · редакторы и инструменты · профилирование

[![услуги](https://img.shields.io/badge/услуги-teivrim.github.io-5eead4?style=for-the-badge)](https://teivrim.github.io)
[![Telegram](https://img.shields.io/badge/Telegram-@TEIVRIM-2AABEE?style=for-the-badge)](https://t.me/TEIVRIM)

</div>

---

## Что делаю

| Услуга | От |
|---|---|
| Геймплей-программист UE5 (C++): StateTree, EQS, AI-контроллеры | 25 000 ₽ |
| Инструменты и редакторы на C++/OpenGL под проект | 40 000 ₽ |
| Профилирование и починка производительности | 15 000 ₽ |
| Обучение C++-разработчиков Rust | 20 000 ₽ |
| Разбор и перенос легаси-кода | 12 000 ₽ |

Подробнее: **[teivrim.github.io](https://teivrim.github.io)**

---

## Портфолио

Не скриншоты — исходники. Каждый проект собирается одной командой, лицензия MIT.
Полное описание и статус сборки: **[портфолио](https://teivrim.github.io/proof.html)**

### [rust-course](https://github.com/Teivrim/rust-course)
Rust с нуля до движка. 20 модулей, **14 912 строк, ноль зависимостей** — только `std`.
Каждый модуль — отдельная программа, харнесс ловит `todo!()` через `catch_unwind` и ставит оценку.
Таблица соответствия C++ → Rust из 51 перевода. `cargo build --release` → 20 бинарников за 15 с.

### [PolygonEditor](https://github.com/Teivrim/PolygonEditor)
3D-редактор сцен на C++17 / OpenGL. Импорт FBX через Assimp, два рендер-бэкенда
(GLFW/OpenGL для сцены, Win32/GDI+ для интерфейса), CMake, сборка **без сети** —
зависимости вендорёны. `cmake -B build && cmake --build build`.

### [NovellEngine](https://github.com/Teivrim/NovellEngine)
Редактор визуальных новел на C++20 / Win32. Таймлайн, панель скрипта, инспектор,
undo/redo на уровне команд, snap-to-grid, свой формат проекта `.vne`.
**Ноль сторонних библиотек** — только системные Win32. `build.bat`.

### [TDEvuris](https://github.com/Teivrim/TDEvuris)
Набор Windows-сканеров на C++17: boot, memory, network, registry, shredder, hasher,
эвристики, подписи, updater. 13 отдельных бинарников вместо монолита.
Ноль зависимостей, чистый Win32.

| Проект | Строк | Зависим. |
|---|---:|---:|
| rust-course | 14 912 | **0** |
| PolygonEditor | 3 801 | 4 |
| NovellEngine | 3 319 | **0** |
| TDEvuris | 3 253 | **0** |

**25 285 строк оригинального кода, copyleft нет нигде.**

---

## Принципы

- **Сначала критерии приёмки.** Если задача сформулирована как «сделай, чтобы работало» — говорю об этом сразу, а не после.
- **Не беру задачу, если не влезает в бюджет.** Предлагаю, что урезать. Не делаю наполовину.
- **Отдаю то, что собирается.** Сборка одной командой у заказчика, а не «у меня работает».
- **Ноль телеметрии.** Код не ходит в сеть за спиной, не требует активации, не звонит домой.
- **Показываю неудачу тоже.** В репозиториях лежит `BUILD-REPORT.md` с реальным результатом сборки,
  включая то, что не собралось и почему.

---

<div align="center">

**[Написать в Telegram](https://t.me/TEIVRIM)** · [услуги и портфолио](https://teivrim.github.io)

</div>
