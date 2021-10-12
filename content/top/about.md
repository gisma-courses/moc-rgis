---
{}
---
# blahblah

R version 4.1.1 (2021-08-10) -- "Kick Things"
Copyright (C) 2021 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

> blogdown:::serve_site()

==> Found hugo at "/home/creu/.local/share/Hugo/0.88.1/hugo" and "/home/creu/bin/hugo". The former will be used. If you don't need both copies, you may delete/uninstall the latter with your system package manager such as apt or yum.

Launching the server via the command:
  /home/creu/.local/share/Hugo/0.88.1/hugo server --bind 127.0.0.1 -p 4321 --themesDir themes -t hugo-theme-cleanwhite -D -F --navigateToChanged
Serving the directory . at http://localhost:4321/moc-rgis/
Launched the hugo server in the background (process ID: 126693). To stop it, call blogdown::stop_server() or restart the R session.
> blogdown::build_site()
Start building sites … 
hugo v0.88.1-5BC54738+extended linux/amd64 BuildDate=2021-09-04T09:39:19Z VendorInfo=gohugoio
WARN 2021/10/12 12:29:42 Page.URL is deprecated and will be removed in a future release. Use .Permalink or .RelPermalink. If what you want is the front matter URL value, use .Params.url
WARN 2021/10/12 12:29:42 Page.UniqueID is deprecated and will be removed in a future release. Use .File.UniqueID
WARN 2021/10/12 12:29:42 Page.Dir is deprecated and will be removed in a future release. Use .File.Dir
.File.UniqueID on zero object. Wrap it in if or with: {{ with .File }}{{ .UniqueID }}{{ end }}
.File.Dir on zero object. Wrap it in if or with: {{ with .File }}{{ .Dir }}{{ end }}

                   | EN   
-------------------+------
  Pages            |  16  
  Paginator pages  |   0  
  Non-page files   |   0  
  Static files     | 947  
  Processed images |   0  
  Aliases          |   1  
  Sitemaps         |   1  
  Cleaned          |   0  

Total in 418 ms