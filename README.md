# Ruby Introduction

Source for the standalone Ruby book at
<https://wintermeyer-consulting.de/ruby/book/>.

The initial content was lifted from the Ruby Introduction chapter of
[_Learn Ruby on Rails_](https://github.com/wintermeyer/rails-book)
and split page-per-section so each topic has its own URL. The Rails
book used to render the same text at
`/rails/book/ruby-basics.html`; that URL now 301-redirects here.

The book has since grown beyond the original Rails chapter. It now
also covers: more String and Hash methods, Symbols, logical
operators, `case/when`, safe navigation `&.`, keyword arguments,
multiple assignment and the splat operator, blocks/Procs/Lambdas,
regular expressions, modules and mixins, and Date/Time.

## Chapters

1. Welcome
2. Ruby 4.0
3. Basics
4. Ruby is Object-Oriented
5. Basic Classes (String, Symbol, Numbers, Boolean, nil)
6. Variables
7. Methods Once Again (method chaining, getters/setters, keyword args, splat, blocks)
8. if-Condition (if/elsif/else, logical operators, case/when, safe navigation)
9. Loops
10. Arrays and Hashes
11. Range
12. Regular Expressions
13. Modules and Mixins
14. Date and Time

## Build

The book is built with [Antora](https://antora.org). The chrome
(Tailwind v4 theme, sidebar, right TOC, pagination, mobile nav)
comes from the shared UI bundle at
[`wintermeyer/wincon-antora-ui`](https://github.com/wintermeyer/wincon-antora-ui).

```sh
npm install
npx antora --fetch antora-local-playbook.yml
```

Open `build/site/book/index.html` to preview.

## Deployment

Pushing to `main` triggers `.github/workflows/deploy.yml`, which
runs on the self-hosted runner `bremen2-eliph-ruby-book` on
bremen2. The runner fetches the wincon nav/footer (stamping
`data-book-current="ruby"`), renders with Antora, copies into
`/var/www/ruby-book/releases/<ts>/`, and atomically swaps the
`current` symlink. Nginx serves `/ruby/book/` from there.

Before the swap the deploy pre-compresses every text asset
(`.html`, `.css`, `.js`, `.svg`, `.xml`, `.json`, `.mjs`, `.txt`,
`.map`) into `.br` (brotli q11) and `.gz` (gzip -9) siblings so
nginx's `brotli_static` / `gzip_static` can serve the response
without spending CPU on the hot path. The brotli module is
already loaded site-wide on bremen2 via the wincon vhost.

## Where the content is edited

In this repo, under `modules/ROOT/pages/*.adoc`. The Rails book no
longer has a Ruby chapter — this repo is the one source of truth.

## License

See individual files for attribution.
