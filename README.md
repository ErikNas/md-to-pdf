# Сборка PDF-файла из markdown с помощью pandoc

В репозитории лежит example.md и example.pdf для примера результата генерации pdf.

## Необходимые пакеты

Скорее всего нужны не все пакеты, но я не знаю какие не нужны.

```Bash
sudo apt-get install pandoc
sudo apt-get install pdflatex
sudo apt-get install basictex
sudo apt-get install wkhtmltopdf
sudo apt-get install weasyprint
sudo apt-get install groff
sudo apt-get install ghostscript
sudo apt-get install texlive-latex-base
sudo apt-get install texlive-latex-extra
sudo apt-get install texlive-fonts-extra
sudo apt-get install texlive-fonts-recommended
```

## Сборка без шаблона

```Bash
pandoc "example.md" \
    --highlight-style=zenburn \
    -V linkcolor:blue \
    -V geometry:a4paper \
    -V geometry:margin=2cm \
    -V mainfont="NotoSans-Light" \
    -V monofont="JetBrainsMono-Regular" \
    --table-of-contents \
    --toc-depth=3 \
    -V toc-title="Содержание" \
    --pdf-engine=xelatex \
    --output="example.pdf"
```

Собирается быстро и даже читабельно.

## Сборка по шаблону

Будет более качественно, но более затратный по времени способ.

Разные шаблоны и желательно шрифты можно скачать по ссылке https://github.com/cab-1729/Pandoc-Themes

Наверное есть и более качественные ресурсы, но не нашел.

Для корректной работы в шапку markdown документа нужно добавить следующее:

```md
---
title: "Заголовок статьи для титульного листа"
author: "Список авторов"
date: "Дата"
---

# Далее идут основные заголовки

И тело наполнения статьи...
```

Иначе титульная страница не соберется.

Строка запуска выглядит вот так:

```Bash
pandoc "example.md" \
    --pdf-engine=xelatex \
    --template=template.tex \
    --output="example.pdf"
```

Постарался как можно подробнее описать каждую строчку в **template.tex**,
чтобы при желании можно было самостоятельно внести правки без глубоких знаний TeX/LaTeX.
