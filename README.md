# solidusram.github.io

Personal site: projects and writing. Built with Jekyll, published by GitHub Pages on every push to `main`.

## Writing a post

1. Write it in `_drafts/name.md` (drafts are never published).
2. When it's ready, move it to `_posts/YYYY-MM-DD-name.md`. The date in the file name is the publication date.
3. Commit and push: GitHub builds the site in a minute or two.

Images and videos go in `assets/img/`. Projects on the home page are in `_data/projects.yml`.

## Preview locally

```
bundle config set --local path vendor/bundle   # once
bundle install                                  # once
bundle exec jekyll serve --drafts               # then open http://localhost:4000
```

`--drafts` also shows the drafts, dated today.
