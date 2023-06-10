# tmplr-example

tmplr is a command line tool to expand a Jinja template with variables in a YAML file.

## tmplr-rs

[tmplr-rs](https://github.com/hnakamur/tmplr-rs) is written in Rust and uses [MiniJinja](https://github.com/mitsuhiko/minijinja) template engine library (See [syntax](https://docs.rs/minijinja/latest/minijinja/syntax/index.html)).

### example output

```bash
$ /usr/bin/tmplr --var vars/dev.yaml --tmpl minijinja/main.j2 
Hello MiniJinja.

- [ ] Do something on the following servers.

  * sv01-osk.dev.example.jp: 10
  * sv02-osk.dev.example.jp: 20
```

```bash
$ /usr/bin/tmplr --var vars/production.yaml --tmpl minijinja/main.j2 
Hello MiniJinja.

- [ ] Do something on the following servers.

  * sv01-osk.example.jp: 20
  * sv02-osk.example.jp: 30
  * sv03-osk.example.jp: 10

- [ ] Do something more only for production.
```

## tmplr

[tmplr](https://github.com/hnakamur/tmplr) is written in Go and uses [pongo2](https://github.com/flosch/pongo2) template engine library.

### example output

```bash
$ ~/go/bin/tmplr -var vars/dev.yaml -tmpl pongo2/main.j2 
Hello pongo2.

- [ ] Do something on the following servers.

  * sv01-osk.dev.example.jp: 10
  * sv02-osk.dev.example.jp: 20
```

```bash
$ ~/go/bin/tmplr -var vars/production.yaml -tmpl pongo2/main.j2 
Hello pongo2.

- [ ] Do something on the following servers.

  * sv01-osk.example.jp: 20
  * sv02-osk.example.jp: 30
  * sv03-osk.example.jp: 10

- [ ] Do something more only for production.
```


## syntax difference between MiniJinja and pongo2

pongo2 has syntax similar to Django, but syntaxes for `import` and `macro` are little different. Maybe there are more differences which I don't know.

### import

MiniJinja

```
{% from "lib/sv_list.j2" import servers_in_zone -%}
```

pongo2

```
{% import "lib/sv_list.j2" servers_in_zone -%}
```

### macro definition start line

MiniJinja

```
{%- macro servers_in_zone(zone) %}
```

pongo2

```
{%- macro servers_in_zone(zone) export %}
```

