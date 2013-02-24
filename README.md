# Meskarune's Letterpress Fork
Letterpress is a minimal, [Markdown](http://daringfireball.net/projects/markdown/) based blogging system written in Python.

#Arch Linux Installation

Install required dependancies, save blog template files to ~/Documents/letterpress and save the letterpress.py file to /usr/local/bin.
```
pacman -S python-pyinotify python-pygments python-markdown

mkdir ~/Documents/letterpress

cd ~/git
git clone https://github.com/meskarune/Letterpress.git

cp ~/git/Letterpress.git/press/* ~/Documents/letterpress
cp ~/git/Letterpress.git/code/letterpress.py /usr/local/bin/letterpress.py
```
Edit the configuration file in ~/Documents/letterpress/letterpress.conf

###Systemd Unit File:

    [Unit]
    Description=Letterpress Blog Post Listener
 
    [Service]
    ExecStart=/usr/bin/python /usr/local/bin/letterpress.py /home/meskarune/Documents/letterpress
 
    [Install]
    WantedBy=multi-user.target



# How It Works
After launch, Letterpress monitors Markdown files(recognized by the filename extension specified in `letterpress.config`) in *press_folder*. When an new Markdown file is detected Letterpress generates a new HTML file from that Markdown file. Similarly, when an existing Markdown file is updated or deleted, Letterpress updates or deletes the corresponding HTML file.

Letterpress also monitors templates. If any change is detected in any of the template files, Letterpress rebuilds the whole site.

Letterpress also monitors subfolders and other files in *press_folder* but treat them as assets. It maps them directly into `site_dir`. It means if you make an *assets* folder and put images there you can reference them in your posts, e.g., `![Big Headshot](/assets/big_headshot.jpg)`.

Letterpress builds these indices automatically:

* Home index
* Archive indices
* Monthly indices
* Yearly indices
* Tag indices

Letterpress writes logs into *press_folder* so you can easily review what is going on.

# Writing
You write posts in such a natural format:
```
title: Post Title
date: Publishing date in the format specified in letterpress.config. The default format is 01/31/2013.
excerpt: Summary of the post.
tags: math, web

Content of the post…

### Let's have fun with math & physics

$E=m*c^2$

```

Refer to `press/sample_post.md` for a complete example.

# Naming
The recommended naming scheme for post files is to use post title, directly or shortened. Adding date to file names would result in redundant path segment in permalinks since Letterpress already puts the HTML files under folders named after their publish dates.

# Credits
* Letterpress originally created by [An0](https://github.com/an0/Letterpress)
* Templates and style sheets are derived from [Michiel de Graaf's blog](https://github.com/michieldegraaf/blog).
* [pyinotify](https://github.com/seb-m/pyinotify) by Sebastien Martini.
* [python-markdown2](https://github.com/trentm/python-markdown2) by Trent Mick. My [fork](https://github.com/an0/python-markdown2) is used here because:

	1. Some necessary bug fixes are not merged back yet.
	2. Some extension is required to support ASCIIMathML embedding.
	3. I want to use my inline-styled footnotes.

* [Pygments](http://pygments.org) by Pocoo.
* [MathJax](http://www.mathjax.org) for [ASCIIMathML](http://www1.chapman.edu/~jipsen/mathml/asciimath.html) processing and [MathML](http://www.mathjax.org) rendering.

So I hardly did any thing but glue these awesome things together.
