# Как настроить открытый репозиторий PRO-Edit

Пошаговая инструкция для владельца. Файлы шаблонов уже лежат в этой папке
(`Z:\Разработка\PRO-Edit-public`). Их нужно **закоммитить и запушить** на GitHub,
затем включить Discussions / Issues в настройках сайта.

Закрытый репозиторий исходников: `KKwer1/PRO-Edit-close`  
Открытый (этот): `KKwer1/PRO-Edit`

---

## 0. Загрузить файлы на GitHub

Если вы ещё не отправили шаблоны в открытый репозиторий:

```powershell
cd "Z:\Разработка\PRO-Edit-public"
git add README.md DISCUSSIONS_WELCOME.md GITHUB_SETUP.md .github
git commit -m "Шаблоны Issues/Discussions, README и инструкция"
git push
```

После push файлы появятся на https://github.com/KKwer1/PRO-Edit

### Что куда попало

| Локальный файл | На GitHub | Зачем |
| --- | --- | --- |
| `README.md` | корень репозитория | Главная страница |
| `DISCUSSIONS_WELCOME.md` | корень (для вас) | Текст приветствия — **скопировать** в Discussions |
| `GITHUB_SETUP.md` | корень (для вас) | Эта инструкция; можно удалить после настройки |
| `.github/ISSUE_TEMPLATE/bug.yml` | Issues → шаблон ошибки | Форма «Сообщить о проблеме» |
| `.github/ISSUE_TEMPLATE/feature.yml` | Issues → шаблон идеи | Форма «Предложить улучшение» |
| `.github/ISSUE_TEMPLATE/config.yml` | Issues → chooser | Без пустых issues + ссылки |
| `.github/DISCUSSION_TEMPLATE/q-a.yml` | Discussions → Q&A | Форма вопроса |
| `.github/DISCUSSION_TEMPLATE/ideas.yml` | Discussions → Ideas | Форма идеи |
| `.github/DISCUSSION_TEMPLATE/announcements.yml` | Discussions → Announcements | Форма анонса |
| `.github/SUPPORT.md` | вкладка Community | Куда писать |
| `.github/SECURITY.md` | Security policy | Как сообщать об уязвимостях |

---

## 1. Описание репозитория (About)

1. Откройте https://github.com/KKwer1/PRO-Edit  
2. Справа нажмите шестерёнку у блока **About**.  
3. Description: `Сборки PRO Edit — помощник редактора объявлений ТРК «Ритм»`  
4. Website (по желанию): `https://github.com/KKwer1/PRO-Edit`  
5. Topics: `windows`, `radmir`, `pro-edit`  
6. Снимите галку **Releases** в About только если не используете Releases; пока релизы лежат файлами в корне — это нормально.  
7. Save.

---

## 2. Включить Issues

1. https://github.com/KKwer1/PRO-Edit → **Settings**  
2. Слева **General** → раздел **Features**  
3. Включите **Issues**  
4. Сохранять отдельно не нужно — переключатель сразу активен.

После push файлов из `.github/ISSUE_TEMPLATE/` при создании Issue появится выбор:

- «Сообщить о проблеме»
- «Предложить улучшение»
- ссылки на Discussions и скачивание  

Пустой issue без шаблона у обычных пользователей скрыт (`blank_issues_enabled: false`).

### Метки (Labels)

1. Вкладка **Issues** → **Labels** (или Settings → Labels)  
2. Создайте, если нет:

| Имя | Цвет (пример) | Описание |
| --- | --- | --- |
| `bug` | `#d73a4a` | Ошибка |
| `enhancement` | `#a2eeef` | Улучшение |
| `question` | `#d876e3` | Вопрос |
| `needs-info` | `#fbca04` | Нужны детали |
| `duplicate` | `#cfd3d7` | Дубликат |

Шаблоны сами вешают `bug` / `enhancement` / `question` — метки должны существовать.

---

## 3. Включить Discussions

1. **Settings** → **General** → **Features**  
2. Включите **Discussions**  
3. GitHub может предложить создать Welcome discussion — можно согласиться или создать вручную (шаг 5).

### Категории Discussions

1. Вкладка **Discussions** → справа **Edit** / **Manage categories** (иконка шестерёнки)  
2. Создайте или переименуйте так, чтобы **slug** совпал с именами файлов:

| Название категории | Slug (важно!) | Тип | Кто пишет |
| --- | --- | --- | --- |
| Announcements | `announcements` | Announcement | только maintainers |
| Q&A | `q-a` | Q&A (с ответами) | все |
| Ideas | `ideas` | Open-ended | все |
| General | `general` | Open-ended | все |

Если slug другой (например, `announcements-1`), либо переименуйте категорию, либо переименуйте файл  
`.github/DISCUSSION_TEMPLATE/<slug>.yml` под фактический slug и снова сделайте push.

---

## 4. Вставить текст для обсуждений (приветствие)

1. Откройте локально файл `DISCUSSIONS_WELCOME.md`  
2. Скопируйте текст **под** разделителем `---` (блок «Добро пожаловать…»)  
3. На GitHub: **Discussions** → **New discussion**  
4. Категория: **Announcements**  
5. Заголовок: `Добро пожаловать в PRO Edit`  
6. Вставьте скопированный текст  
7. Create discussion  
8. Справа у обсуждения: **Pin discussion** (закрепить), чтобы оно было сверху.

Это и есть «текст для GitHub для обсуждений».

---

## 5. Безопасность

1. **Settings** → **Code security** (или **Security**)  
2. Включите **Private vulnerability reporting**, если доступно  
3. Файл `.github/SECURITY.md` уже задаёт политику на вкладке Security.

---

## 6. Рекомендуемые настройки открытого репозитория

| Настройка | Рекомендация |
| --- | --- |
| Visibility | Public |
| Wiki | Off |
| Projects | Off (если не используете) |
| Issues | On |
| Discussions | On |
| Actions | Off или только для публикации (исходников здесь нет) |
| Branch protection `main` | Запрет force push и удаления ветки |
| Содержимое | Только сборки (`exe`, `rar`, `latest.json`) + docs/шаблоны. **Никогда** исходники, `.env`, ключи |

### Как публиковать новую версию (сейчас)

1. Собрать в закрытом проекте: `npm run release`  
2. Скопировать `PRO Edit.exe` → `PRO-Edit.exe`, архив → `PRO-Edit.rar`  
3. Обновить `latest.json` (version, url, sha256, notes)  
4. Commit + push в `PRO-Edit`  

URL в `latest.json` сейчас:

`https://raw.githubusercontent.com/KKwer1/PRO-Edit/main/PRO-Edit.exe`

### Позже (по желанию): GitHub Releases

Создавать Release с тегом `v1.2.0` и прикреплять rar/exe удобнее для людей, но тогда нужно поменять `url` в `latest.json` на ссылку из Release Assets и URL в программе обновления.

---

## 7. Рекомендации для закрытого репозитория `PRO-Edit-close`

| Настройка | Рекомендация |
| --- | --- |
| Visibility | Private |
| Issues / Discussions | Off — вся обратная связь в открытом |
| Branch protection `main` | PR + запрет force push |
| Dependabot alerts | On |
| Secret scanning / push protection | On (если доступно) |
| Секреты в Git | Никогда; только GitHub Secrets |

SSH remotes (порт 22 часто закрыт — используем 443):

- origin: `ssh://git@ssh.github.com:443/KKwer1/PRO-Edit-close.git`  
- public: `ssh://git@ssh.github.com:443/KKwer1/PRO-Edit.git`

---

## 8. Проверка, что всё работает

1. https://github.com/KKwer1/PRO-Edit — виден README и файлы rar/exe  
2. **New issue** — предлагаются два шаблона  
3. **New discussion** в Q&A — форма с полями версии и вопроса  
4. Закреплённое приветствие в Announcements  
5. Ссылка «Сообщить о проблеме» из README открывает форму бага
