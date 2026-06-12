# Remotion Skills — установка и использование

Набор **Agent Skills** для создания видео на [Remotion](https://www.remotion.dev/) (React + программный рендер). Один публичный скилл с десятками тематических правил + отдельные внутренние скиллы для контрибьюторов монорепозитория.

**Важно:** скиллы работают с AI-агентом, не с редактором. VS Code сам по себе скиллы не читает — нужен Copilot, Cline, Continue и т.д.

**Upstream:** `remotion-dev/remotion` (монорепо) · публичный пакет скиллов: [`remotion-dev/skills`](https://github.com/remotion-dev/skills) (зеркало `packages/skills/`).

---

## Два уровня скиллов

| Уровень | Где лежит | Кому нужен |
|---------|-----------|------------|
| **Публичный** `remotion-best-practices` | `packages/skills/skills/remotion/` | Всем, кто делает видео в Remotion |
| **Внутренние** (18 шт.) | `.agents/skills/` в корне монорепо | Только контрибьюторам Remotion |

Если ты **не** разрабатываешь сам фреймворк — тебе нужен только публичный скилл. Внутренние (PR, issues, add-effect, writing-docs…) — для команды Remotion внутри этого репозитория.

---

## Публичный скилл

### remotion-best-practices
Учит агента писать **правильный Remotion-код**: анимации через `useCurrentFrame()` и `interpolate()`, `<Sequence>`, `<Composition>`, медиа, субтитры, эффекты, 3D и т.д.

**Ключевые ограничения из скилла:**
- CSS transitions/animations и Tailwind animation-классы **запрещены** — в рендере они не работают;
- анимировать через `interpolate()` в `style`, предпочитать отдельные свойства (`scale`, `translate`, `rotate`);
- ассеты — в `public/`, ссылки через `staticFile()`;
- новый проект: `npx create-video@latest --yes --blank --no-tailwind my-video`;
- превью: `npx remotion studio`.

**Тематические правила** (агент подгружает по задаче из `packages/skills/skills/remotion/rules/`):

### Основы, тайминг, структура
| Правило | Что покрывает |
|---------|----------------|
| `video-layout.md` | Вёрстка под видео: размеры текста, сцены, промо |
| `timing.md` | `interpolate`, easing, springs |
| `sequencing.md` | Задержки, обрезка, длительность через `<Sequence>` |
| `trimming.md` | Обрезка начала/конца анимаций |
| `compositions.md` | Stills, папки, default props, вложенные композиции |
| `parameters.md` | Параметризация через Zod-схему |
| `calculate-metadata.md` | Динамическая длительность, размеры, props |

### Медиа
| Правило | Что покрывает |
|---------|----------------|
| `images.md` | Картинки: размер, позиция, динамические пути |
| `videos.md` | Видео: trim, volume, speed, loop, pitch |
| `gifs.md` | GIF, синхронизация с таймлайном |
| `audio.md` | Продвинутое аудио: trim, volume, speed, pitch |
| `transparent-videos.md` | Рендер с прозрачностью |

### Текст, шрифты, UI
| Правило | Что покрывает |
|---------|----------------|
| `text-animations.md` | Typewriter, подсветка слов (+ примеры `.tsx` в `rules/assets/`) |
| `measuring-text.md` | Измерение текста, overflow |
| `measuring-dom-nodes.md` | Размеры DOM-элементов |
| `google-fonts.md` | Google Fonts (рекомендуемый способ) |
| `local-fonts.md` | Локальные шрифты |
| `tailwind.md` | Tailwind в Remotion (без animation-классов) |

### Субтитры и озвучка
| Правило | Что покрывает |
|---------|----------------|
| `subtitles.md` | Формат `Caption`, общий пайплайн |
| `transcribe-captions.md` | Транскрипция → captions |
| `display-captions.md` | Отображение субтитров |
| `import-srt-captions.md` | Импорт SRT |
| `voiceover.md` | AI voiceover через ElevenLabs TTS |

### Эффекты и визуал
| Правило | Что покрывает |
|---------|----------------|
| `effects.md` | `@remotion/effects`: blur, glow, halftone, vignette и др. |
| `light-leaks.md` | Light leak оверлеи |
| `html-in-canvas.md` | Кастомная отрисовка через `<HtmlInCanvas>` |
| `audio-visualization.md` | Спектр, waveform, bass-reactive |
| `sfx.md` | Звуковые эффекты |
| `3d.md` | Three.js / React Three Fiber |
| `lottie.md` | Lottie-анимации |
| `maplibre.md` | Карты с маршрутами и flyover |
| `transitions.md` | `TransitionSeries`: fade, slide, wipe, overlays |

### Утилиты и FFmpeg
| Правило | Что покрывает |
|---------|----------------|
| `ffmpeg.md` | Trim, нарезка через FFmpeg |
| `silence-detection.md` | Обрезка тишины |
| `get-audio-duration.md` | Длительность аудио (Mediabunny) |
| `get-video-duration.md` | Длительность видео |
| `get-video-dimensions.md` | Ширина/высота видео |

**Промпты — новый ролик:**
```
remotion-best-practices: создай 15-секундный promo для SaaS — fade in заголовка и CTA
```
```
Сделай animated bar chart на 5 столбцов в Remotion
```

**Промпты — субтитры и аудио:**
```
remotion-best-practices: добавь captions и фоновую музыку к этой композиции
```
```
Транскрибируй voiceover.mp3 и покажи субтитры синхронно с таймлайном
```

**Промпты — эффекты и переходы:**
```
Добавь light leak между сценами через TransitionSeries
```
```
Примени vignette и chromaticAberration к intro-сцене
```

**Промпты — отладка:**
```
Почему CSS animation не работает в Remotion? Исправь на interpolate()
```
```
npx remotion still MyComp --frame=30 — проверь layout на 1-й секунде
```

---

## Внутренние скиллы (только для контрибьюторов монорепо)

Лежат в `.agents/skills/`. Имеют смысл, если ты **вносишь изменения в сам Remotion**, а не просто делаешь видео в своём проекте.

| Скилл | Что делает |
|-------|------------|
| `add-effect` | Новый эффект в `@remotion/effects` + доки + обновление публичного скилла |
| `add-sfx` | Новый звук в `@remotion/sfx` |
| `add-cli-option` | Новая CLI/config опция |
| `add-new-package` | Новый пакет `@remotion/*` в монорепо |
| `add-expert` | Запись на странице experts |
| `writing-docs` | Написание MDX-документации |
| `docs-demo` | Интерактивный `<Demo>` в доках |
| `visual-mode` | Remotion Studio Visual Mode |
| `web-renderer-test` | Тест для web renderer |
| `video-report` | Отчёт по видео |
| `pr` / `pr-name` / `pr-ready` | Pull request: создание, название, доведение до merge |
| `issue` / `issue-management` | GitHub issues и связи между ними |
| `fix-dependabot` | Починка Dependabot PR в монорепо |
| `update-version` / `version` | Версионирование Remotion |

---

## Установка

### Требования

- **Node.js** (для `npx` и Remotion-проекта)
- Для самого видео — Remotion-проект (`npx create-video@latest`)

### Публичный скилл — в проект (рекомендуется)

```bash
cd /path/to/your-remotion-project

# официальный способ (через отдельный репозиторий скиллов)
npx skills add remotion-dev/skills -a cursor -y

# обёртка Remotion CLI (прокидывает аргументы в skills CLI)
npx remotion skills add -- -a cursor -y
```

При создании проекта скиллы можно включить в мастере:

```bash
npx create-video@latest --yes --blank my-video
cd my-video
npm i
npx remotion skills add
```

| Область | Флаг | Куда |
|---------|------|------|
| Проект | без `-g` | `.agents/skills/` |
| Глобально | `-g` | `~/.agents/skills/` |

Remotion также создаёт symlink'и для Claude Code в `.claude/skills/`.

### Из локального клона монорепо (без GitHub)

Копируй папку скилла целиком — вместе с `rules/`:

```bash
cd /path/to/your-remotion-project

mkdir -p .agents/skills
cp -r /path/to/remotion/packages/skills/skills/remotion .agents/skills/remotion-best-practices
```

### Cursor + VS Code сразу

```bash
cd /path/to/your-remotion-project

npx skills add remotion-dev/skills \
  -a cursor -a github-copilot -y
```

| Агент в VS Code | Флаг `--agent` | Папка |
|-----------------|----------------|-------|
| GitHub Copilot | `github-copilot` | `.agents/skills/` |
| Cline | `cline` | `.agents/skills/` |
| Continue | `continue` | `.continue/skills/` |
| Roo Code | `roo` | `.roo/skills/` |

### Глобально (на все проекты)

```bash
npx -y skills@latest add remotion-dev/skills -g -a cursor -y
```

### Внутренние скиллы контрибьютора

Уже лежат в клоне монорепо: `remotion/.agents/skills/`. Для работы в этом репозитории открывай **корень монорепо** как проект в Cursor — агент увидит их автоматически. В свой видео-проект их копировать не нужно.

### Флаги

| Флаг | Значение |
|------|----------|
| `-y` / `--yes` | Без вопросов в терминале |
| `-g` / `--global` | На все проекты |
| `-a` / `--agent` | Целевой агент (`cursor`, `github-copilot`, …) |

### Удалить

```bash
# публичный скилл
npx skills remove remotion-best-practices -a cursor -y

# вручную
rm -rf .agents/skills/remotion-best-practices
rm -rf .agents/skills/remotion
```

### Обновить

```bash
npx remotion skills update
# или
npx skills update
npx skills list
```

---

## Использование

1. Создай или открой **Remotion-проект** (не весь монорепо, если цель — своё видео).
2. Установи публичный скилл в `.agents/skills/`.
3. Запусти Studio для превью: `npx remotion studio` (или `npm run dev`).
4. В чате агента опиши сцену/ролик; агент подхватывает скилл по `description` и читает нужные `rules/*.md`.

**Типичный порядок с другими скиллами:**
```
remotion-best-practices  →  код видео, анимации, рендер
ui-ux-pro-max / absolute-ui →  визуальный стиль сцен (если нужен design system)
stop-slop                →  тексты в ролике без AI-slop
copywriting              →  маркетинговый copy для promo
absolute-documentations  →  README / how-to по проекту
```

**Когда какой скилл:**
- `remotion-best-practices` — **любой Remotion-код** (анимации, рендер, медиа)
- `ui-ux-pro-max` — палитры и UI-паттерны для веба; для motion graphics часто достаточно Remotion-скилла
- `stop-slop` — озвучка/титры **текстом**, не код

`.agents/skills/` можно закоммитить в git — команда получит те же инструкции для агента.

---

## Что ещё в каталоге `remotion/`

Это **полный монорепозиторий фреймворка**, не только скиллы:

| Путь | Содержание |
|------|------------|
| `packages/remotion`, `packages/cli`, … | Исходники Remotion |
| `packages/skills/` | Публичный Agent Skill |
| `packages/skills-evals/` | Тесты качества скиллов (внутреннее) |
| `packages/codex-plugin/` | Плагин для OpenAI Codex |
| `packages/template-prompt-to-motion-graphics/` | Шаблон «промпт → motion graphics» со своей системой skills |
| `.agents/skills/` | Скиллы для контрибьюторов |

Документация: https://www.remotion.dev/docs/ai/skills
