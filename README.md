# Сайт проекта CoreBus

## Как добавить новую карточку на страницу загрузок

Редактируется файл `downloads.html`.

Все версии находятся внутри блока `<div class="version-list">`. Каждая версия — это отдельная карточка `<article class="version-card">`. Карточки расположены от новой к старой: **самая свежая версия — первая**.

### Как добавить новую версию

#### 1. Скопировать карточку

Найти первую карточку в списке (сейчас это версия с классом `version-card--current`).

Скопировать её **целиком** — от открывающего `<article class="version-card version-card--current">` до закрывающего `</article>`.

Вставить копию **перед** этой карточкой, сразу после `<div class="version-list">`.

#### 2. Отметить новую версию как «последняя»

В **новой** (верхней) карточке оставить класс `version-card--current`:

```html
<article class="version-card version-card--current">
```

В **предыдущей** последней версии убрать `version-card--current`:

```html
<article class="version-card">
```

Этот класс включает зелёную рамку и бейдж «Последняя версия». Он должен быть только у одной карточки — у самой новой.

#### 3. Шапка карточки

В блоке `<header class="version-card__header">` изменить:

- **Номер версии** — текст внутри `<span class="version-card__version">`, например `3.6.0`.
- **Дату** — в `<time class="version-card__date">`:
  - атрибут `datetime` в формате `2026-07-01`;
  - текст даты, например `1 июля 2026`.

Бейдж `<span class="version-card__badge">Последняя версия</span>` не изменять — он есть во всех карточках, но виден только у отмеченной `version-card--current`.

#### 4. Блок «Что нового?»

Блок `<details class="version-card__changelog">`:

- у **новой** версии добавить атрибут `open` — changelog будет раскрыт:
  ```html
  <details class="version-card__changelog" open>
  ```
- у **всех остальных** карточек атрибут `open` убрать.

Список изменений — пункты `<li>` внутри `<ul>`. Если изменений нет, оставить:

```html
<p class="version-card__changelog-empty">—</p>
```

#### 5. Блок «Загрузки»

В `<div class="version-card__downloads">` обновить ссылки на файлы.

Структура блока:

```
Загрузки
├── Windows (section platform-block--windows)
│   ├── Installer x64  → кнопки загрузки
│   └── Portable x64   → кнопки загрузки
└── Linux (section platform-block--linux)
    └── Portable x64   → кнопки загрузки
```

Секции Windows и Linux копировать не нужно — они уже есть в карточке. Меняются только ссылки в кнопках.

Каждая кнопка — это строка вида:

```html
<a class="download-btn download-btn--yandex" href="ССЫЛКА" title="CoreBus_3.6.0_win_x64_installer"></a>
```

В каждой кнопке заменить:

- `href` — ссылку на файл или папку на зеркале;
- `title` — имя файла по шаблону:

| Строка | Значение title |
|---|---|
| Windows → Installer x64 | `CoreBus_{версия}_win_x64_installer` |
| Windows → Portable x64 | `CoreBus_{версия}_win_x64_portable` |
| Linux → Portable x64 | `CoreBus_{версия}_linux_x64` |

Типы кнопок (класс после `download-btn`):

| Класс | Зеркало |
|---|---|
| `download-btn--yandex` | Яндекс.Диск |
| `download-btn--gdrive` | Google Drive |
| `download-btn--sourceforge` | SourceForge |

Не у каждой версии должны быть все три зеркала. Если ссылки на Google Drive нет — удалить соответствующую кнопку `download-btn--gdrive` из строки.

Для SourceForge ссылка строится по шаблону:

```
https://sourceforge.net/projects/corebus/files/CoreBus_{версия}_win_x64_installer.exe/download
https://sourceforge.net/projects/corebus/files/CoreBus_{версия}_win_x64_portable.zip/download
https://sourceforge.net/projects/corebus/files/CoreBus_{версия}_linux_x64.zip/download
```

#### 6. Проверка

После сохранения проверить:

- новая карточка стоит **первой** в списке;
- `version-card--current` только у новой версии;
- `open` на changelog только у новой версии;
- номер версии, даты, ссылки и `title` у кнопок соответствуют новой версии;
- страница корректно отображается в браузере.

### Что не нужно менять

- `style.css` — стили уже настроены.
- Подписи «Windows», «Linux», «Яндекс.Диск» и иконки на кнопках — подставляются автоматически.
- Заголовок «Загрузки» с иконкой — копируется вместе с карточкой без изменений.
