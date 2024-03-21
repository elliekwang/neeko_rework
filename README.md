# neeko_rework
UCSD DSC 80 Project - League of Legends

<!DOCTYPE html>
<html lang="{{ page.lang | default: site.lang | default: "en" }}">

<head>
    <meta charst = "UTF-8">
  {%- include head.html -%}

<head>
  <body>

    {%- include header.html -%}

    <main class="page-content" aria-label="Content">
      <div class="wrapper">
        {{ content }}
      </div>
    </main>

    {%- include footer.html -%}

  </body>

</html>
