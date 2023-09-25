# Réunion de rentrée des M1 AMIS, DataScale, IRS et SeCReTS

![Build status](https://github.com/uvsq-info/m1-rentree/actions/workflows/deploy.yml/badge.svg)

## Construction du document
Les outils suivants doivent être installés sur le système.
* [`bundler`](https://bundler.io/)
* [`graphviz`](https://graphviz.org/) (pour les diagrammes)
* [`rake`](https://ruby.github.io/rake/)

### Installation des dépendances (gems)
```
$ bundle install
```

### Construction (à la main)
```
$ # Construction du document
$ bundle exec asciidoctor -r asciidoctor-diagram -D html/ src/index.adoc
$ # Construction des slides
$ wget -qO- https://github.com/hakimel/reveal.js/archive/refs/tags/4.5.0.tar.gz | \
        tar --transform 's/^reveal.js-4.5.0/reveal.js/' -xz -C html
$ mkdir -p html/css && cp src/custom.css html/css
$ bundle exec asciidoctor-revealjs -r asciidoctor-diagram -D html/ -o slides.html src/index.adoc
```

### Construction (avec rake)
```
$ bundle exec rake
```
