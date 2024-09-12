require 'rake/clean'
# rake/clean définit CLEAN (Rake::FileList) pour les fichiers temporaires
# et CLOBBER (Rake::FileList) pour les fichiers de sortie

REVEALJS_VERION = "5.1.0"

# ajoute les fichiers html comme fichiers intermédiaire
CLEAN << "html/index.html"
CLEAN << "html/slides.html"
CLEAN << "html/figs"
CLEAN << "html/css"
# ajoute le répertoire html comme fichier de sortie
CLOBBER << "html"

desc "Génère le document"
task :default => [:init_html, :generate_book, :generate_slides]
# :default est un symbole Ruby
# task <cible> => <dépendances>

desc "Initialise le répertoire de destination des fichiers html"
task :init_html => %w[html/reveal.js html/figs html/css]
directory "html/reveal.js" => "html" do |t|
    sh <<~HEREDOC
        wget -qO- https://github.com/hakimel/reveal.js/archive/#{REVEALJS_VERION}.tar.gz | \
        tar --transform 's/^reveal.js-#{REVEALJS_VERION}/reveal.js/' -xz -C #{t.source}/
    HEREDOC
end

desc "Initialise le répertoire des images"
directory "html/figs" => "html" do |t|
    mkdir_p t.name
    cp Dir["src/figs/*.png", "src/figs/*.svg"], t.name
end

desc "Initialise le répertoire des feuilles de styles CSS"
directory "html/css" => %w[src/custom.css html] do |t|
    mkdir_p t.name
    cp t.source, t.name
end

# directory task pour créer le répertoire
directory "html"

desc "Génère le document"
task :generate_book => [:init_html, "html/index.html"]
# file task
file "html/index.html" => %w[src/index.adoc] do |t|
    sh "asciidoctor -r asciidoctor-diagram -D html/ #{t.source}"
end

desc "Génère les slides"
task :generate_slides => [:init_html, "html/slides.html"]
# file task
file "html/slides.html" => %w[src/index.adoc] do |t|
    sh "asciidoctor-revealjs -r asciidoctor-diagram -D html/ -o slides.html #{t.source}"
end
