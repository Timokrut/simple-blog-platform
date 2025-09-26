# Branching Report

## Merge Statistics
- Total number of merges: 5
- Fast-forward merges: 1
- 3-way merges: 4 
- Merges with conflicts: 2

## Branch History
```bash
*   670087b (HEAD -> main, origin/main) Merge branch 'documentation'
|\
| * 5d6df84 (documentation) documentaion update
|/
*   0d28e26 Merge feature/header-update with conflict resolution
|\
| * ba0157c Update header to v2.0
* | 61b39b5 Customize blog title
|/
*   168e482 Merge branch 'feature/design'
|\
| * 8310259 Improve design and add navigation
* |   e562431 Merge branch 'feature/comments'
|\ \
| |/
|/|
| * fd43389 Add comments section
|/
* 5a7a165 Add posts page and functionality
* b1f3b5f Initial project setup
```

## Lessons Learned
Вроде бы понял все что было про ветки и слияния, но пока выполнял задание, возникло 1(2) проблемы. А именно пункт 16 и 17

### 16
Переключитесь на main и слейте feature/comments (будет 3-way merge).

По дефолту там будет ff, поскольку main мы никак не меняем, после создания ветки, но чтобы получить 3-way merge можно использовать --no-ff, что я и сделал. (по сути это не то чтобы проблема, но по формулировке выглядит так, как будто там должен быть 3-way merge по дефолту)

### 17
После того как мы сделали merge для main и feature/comments, у меня возник конфликт в index.html, поскольку после заголовка мы добавили, поэтому пришлось решить еще и этот конфликт (я просто объединил 2 файла) 
```html
feature/comments
<div class="comments-section">
    <h2>Recent Comments</h2>
    <div id="comments"></div>
</div>

feature/design
<nav class="navigation">
    <a href="index.html">Home</a>
    <a href="posts.html">Posts</a>
</nav>
```

### Логи к п.16 и п.17
```bash
$ git branch
  feature/comments
  feature/design
  feature/posts
* main

$ git log --oneline
5a7a165 (HEAD -> main, feature/posts) Add posts page and functionality
b1f3b5f Initial project setup
user@Timokrut:~/simple-blog-platform$ git merge feature/comments
Updating 5a7a165..fd43389
Fast-forward
 index.html     | 4 ++++
 js/comments.js | 5 +++++
 2 files changed, 9 insertions(+)
 create mode 100644 js/comments.js

$ git merge feature/design
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.

$ cat index.html
<h1>Simple Blog</h1>
<<<<<<< HEAD
<div class="comments-section">
    <h2>Recent Comments</h2>
    <div id="comments"></div>
</div>
=======
<nav class="navigation">
    <a href="index.html">Home</a>
    <a href="posts.html">Posts</a>
</nav>
>>>>>>> feature/design

```
