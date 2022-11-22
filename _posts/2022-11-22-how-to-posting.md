---
title: Blog 포스팅 하기
author: 김도균
date: 2022-11-22 23:37:00 +0900
categories: [스터디, MySQL]
tags: [MySQL, 쿼리, 컴퓨터공학, 데이터베이스]
---

# 1. 레포지토리 클론

```bash
git clone (레포지토리 주소) (원하는 위치)
```

예시:

```bash
git clone https://github.com/NohGod/NohGod.github.io.git .
```

# 2. 새로운 브렌치 만들기

```bash
git checkout -B 브렌치이름
```

예시:

```bash
git checkout -B jasper200207
```

### 여기까지는 처음에만 하면 된다

<br>

# 3. Pull

```bash
git pull origin (브렌치이름)
```

작업시작하기전에 풀 당기고 하는 걸 추천

예시:

```bash
git pull origin jasper200207
```

# 3. 마크다운 파일로 정리하기

노션에 정리하고 다운받아도 괜찮음

# 4. 파일이름정하기

YYYY-MM-DD-title.md 의 형태

title은 title설정 안했을 시에 기본값

`2022-11-22-how-to-posting.md`

# 5. 마크다운 상단에 필요한 내용 넣기

```markdown
---
title: 포스트 제목
author: 작성자 id
date: 작성일 YYYY-MM-DD HH:MI:SS 시차
categories: 카테고리 리스트 [category1, category2] category1/category2로 지정
tags: 태그 리스트 [tag1, tag2, ... ]
---
```

# 6. 마크다운 수정

노션에서 가져왔을 경우 마크다운이 깨지는 경우가 있으니 확인하고 수정

하이퍼링크 정상인지 확인하고 필요없으면 삭제

# 7. 이미지 경로 변경

/assets/img/title로 폴더 만들어서 이미지 가져오기

/assets/img/title/이미지이름.확장자의 형태로 가져오기

예시:

`/assets/img/how-to-posting/bear.png`

![bear.png](/assets/img/how-to-posting/bear.png)

# 8. 푸시하기

## I. add

```bash
git add (포함할 변경한 파일이름)
```

예시:

```bash
git add .
```

## II. commit

```bash
git commit -m "커밋제목" -m "커밋내용"
```

제목만 넣어도 됨

예시:

```bash
git commit -m "posting : Blog 포스팅하기"
```

## III. push

```bash
git push origin (브렌치이름)
```

예시 :

```bash
git push origin jasper200207
```

# 9. PR

## I. 깃허브 레포지토리 접속

## II. Pull requests탭에 New pull request 클릭

![Newpullrequest.PNG](/assets/img/how-to-posting/Newpullrequest.png)

## III. 자기 브렌치 선택 & base main인지 확인

![branch.PNG](/assets/img/how-to-posting/branch.png)

## IV. Create pull request 클릭

![create.PNG](/assets/img/how-to-posting/create.png)

## V. 적절한 코멘트 작성 후 Create pull request 클릭

![msg_create.PNG](/assets/img/how-to-posting/msg_create.png)

## VI. 문제없으면 Merge pull request 클릭

![merge.PNG](/assets/img/how-to-posting/merge.png)
