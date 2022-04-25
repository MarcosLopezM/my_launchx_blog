---
title: "Usando MathJax"
date: 2022-04-25
description: 'Integrando MathJax a nuestro blog'
---

Muchas veces cuando buscamos información sobre algún tema afín a las matemáticas, nos encontramos con páginas web en las que las fórmulas matemáticas no son legibles, ya sea en forma de image o con un formato muy _engorroso_, lo cual es un problema para los lectores.

<figure style="text-align: center;">
  <img syle="display: inline-block; margin-left: auto; margin-right: auto;" src="https://user-images.githubusercontent.com/57697020/165169177-e3755a5a-e027-4f9e-9510-444bed83fa4e.png" alt="Ejemplo de una fórmula mostrada incorrectamente">
  <figcaption>Fórmula mostrada incorrectamente</figcaption>
</figure>

Es por eso que nos interesa integrar [MathJax][mathjax] a nuestro blog, para que los lectores puedan leer las fórmulas matemáticas como si estuvieran leyéndolas en un libro de texto.

Pero...

## ¿Qué es [MathJax][mathjax]?

  > **MathJax** es una librería de javascript que nos permite visualizar
  > fórmulas matemáticas en los navegadores web.

## Usando [MathJax][mathjax] con [Hugo][hugo]

Para usar **MathJax**, lo primero que debemos hacer es importarlo en algún lugar del sitio web. En este caso se importó en el archivo <code>/themes/hugo-winston-theme/layouts/partials/footer.html</code>, ya que este se incluye en cada una de las páginas del blog.  
En nuestro caso tenemos que inialmente el archivo <code>footer.html</code> se ve como:
```html
  <div class="footer">
  {{ if .Site.Data.social.links }}
  <div class="footer-social">
    {{ range .Site.Data.social.links }}
      <span class="social-icon social-icon-{{ .name | urlize }}">
        <a href="{{ .url }}" title="{{ .name }}" target="_blank" rel="noopener">
          <img src="{{ .image | relURL }}" width="24" height="24" alt="{{ .name }}"/>
        </a>
      </span>
    {{ end }}
  </div>
  {{ end }}
</div>
```

Y, agregando las líneas de código que importan todas las funcionalidades de **MathJax**,

```html

<div class="footer">
  {{ if .Site.Data.social.links }}
  <div class="footer-social">
    {{ range .Site.Data.social.links }}
      <span class="social-icon social-icon-{{ .name | urlize }}">
        <a href="{{ .url }}" title="{{ .name }}" target="_blank" rel="noopener">
          <img src="{{ .image | relURL }}" width="24" height="24" alt="{{ .name }}"/>
        </a>
      </span>
    {{ end }}
  </div>
  {{ end }}
</div>

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
```

Es necesario mencionar que **MathJax** genera código **HTML**, el cual no es renderizado por el formato de **MarkDown** (**GoldMark**, formato por defecto usado por **HUGO**). Es por eso que se debe agregar la siguiente línea al archivo `config.toml`:

```
[markup.goldmark.renderer]
  unsafe = true
```

¡Ya estamos listos para escribir estas fórmulas!

## Recreando el código de la imagen

<div>
  \[
    \begin{align*}
      \langle \color{blue}{\textbf{A}} \rangle &= \dfrac{(10 + 8 + 4 + 1)}{5},\\
      &= \dfrac{28}{5},\\
      &= 5.6
    \end{align*}
  \]
</div>

[mathjax]: https://www.mathjax.org/
[hugo]: https://gohugo.io/
