Hwan's Light Blog

## init

```sh
docker run --rm -d -v .:/src klakegg/hugo:0.101.0 new site HwanBlog
cd HwanBlog
git init
git submodule add https://github.com/nanxiaobei/hugo-paper themes/paper
```

add theme on config.yaml

```sh
theme = "paper"
```

test on hugo server

```sh 
docker run --rm -v .:/src -p 1313:1313 klakegg/hugo:0.101.0 server
```

## Posting

add new page
```sh
docker run --rm -v .:/src klakegg/hugo:0.101.0 posts/new my-first-post.md
```
