# templates/ — шаблоны резюме на LaTeX

Здесь лежат **исходные шаблоны** резюме — в том виде, в каком они получены от
авторов, без моих данных. Это «библиотека заготовок»: отсюда берут старт новые
версии резюме в [`resumes/`](../resumes/).

**Шаблоны не редактируем.** Правки идут только в копии внутри `resumes/<версия>/`.
Так всегда видно, что именно я изменил относительно оригинала, и в любой момент
можно начать заново с чистого шаблона.

## Что есть

| Папка | Шаблон | Автор | Источник | Лицензия |
| --- | --- | --- | --- | --- |
| [`jakes_resume/`](jakes_resume/) | Jake's Resume | Jake Gutierrez | [github.com/jakegut/resume](https://github.com/jakegut/resume) · [Overleaf](https://www.overleaf.com/latex/templates/jakes-resume/syzfjbzwjncs) | MIT |
| [`nanu_rezume/`](nanu_rezume/) | Rezume | Nanu Panchamurthy | [github.com/nanupnch/Rezume](https://github.com/nanupnch/Rezume) | MIT |

Оба шаблона — потомки [sb2nov/resume](https://github.com/sb2nov/resume), поэтому
разметка у них похожая: одностраничное ATS-friendly резюме, секции через
`\resumeSubheading` / `\resumeItem`, без внешних шрифтов и картинок.

Текущие резюме в `resumes/` собраны на базе **Rezume**.

В каждой папке шаблона: сам `.tex` и `LICENSE` автора. Лицензии MIT — использовать
и менять можно свободно, важно лишь не выкидывать копирайт-заголовок из `.tex`.

## Как завести новую версию резюме из шаблона

```bash
mkdir -p resumes/<новая_версия>
cp templates/nanu_rezume/rezume.tex resumes/<новая_версия>/Sanzhar_Sovet_resume.tex
```

Имя `.tex` во всех версиях одинаковое — `Sanzhar_Sovet_resume.tex`; версию
определяет папка (см. [AGENTS.MD](../AGENTS.MD)). Дальше — открыть файл в VS Code
и сохранить: LaTeX Workshop соберёт PDF в Docker.

## Проверка сборки шаблона

Шаблоны собираются тем же образом, что закреплён для всего репозитория
(`texlive/texlive:TL2025-historic`). Проверить, что шаблон компилируется как есть:

```bash
cd templates/jakes_resume
docker run --rm -v "$PWD":/w -w /w texlive/texlive:TL2025-historic \
  pdflatex -interaction=nonstopmode resume.tex
```

Обе заготовки проверены на этом образе и собираются без ошибок (1 страница).
Промежуточные артефакты (`.aux`, `.log`, `.out`, `.fls`, …) отсечены корневым
`.gitignore`. Собранный из шаблона PDF — это просто демо, его тоже не коммитим:
в репозитории живут PDF только настоящих резюме из `resumes/`.

## Как добавить сюда новый шаблон

1. Папка `templates/<автор>_<название>/` в snake_case — имя автора спереди,
   чтобы шаблоны не путались между собой и было видно, чьё это (`jakes_resume`,
   `nanu_rezume`).
2. Внутрь — оригинальный `.tex` и файл лицензии автора.
3. Строку в таблицу выше: имя, автор, ссылка на источник, лицензия.
4. Прогнать проверку сборки из раздела выше.
