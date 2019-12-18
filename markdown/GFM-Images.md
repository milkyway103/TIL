Github-Flavored-Markdown에서 이미지 삽입하기
--------------------------------------------

### basic

link를 삽입하는 방식과 거의 비슷하다. 다만 `![`와 `]` 사이에 적은 텍스트가 link text가 아닌, **image description** 이 된다. (html 태그에서의 `alt`\)

```
![foo](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png)
```

라고 쓰면 아래와 같이 이미지가 나타난다. ![foo](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png)

다음과 같이 이미지의 `title` 태그를 추가할 수도 있다.

```
![foo](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png "이것은 깃허브 로고입니다")
```

![foo](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png)

`[`와 `]` 사이에 이미지 주소를 중첩해서 적더라도, 바깥의 링크 하나만 적용된다.

```
![foo ![bar](https://github.githubassets.com/images/modules/logos_page/Octocat.png)](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png)
```

![foo ![bar](https://github.githubassets.com/images/modules/logos_page/Octocat.png)](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png)

하지만 이 태그는 rendering되는 것이 아니라 parsing되는 것으로 간주되기 때문에, HTML으로 렌더링할 때 가장 단순한 형태의 이미지 설명을 사용하는 것이 권장된다. (이미지 설명에 `*`나 `[`, `]` 따위의 리터럴을 사용하지 말 것) 어차피 HTML로 파싱될 때 이러한 연산자들은 누락된다.

### Reference-style

Reference-style로 사용하는 것이 가능하다.

```
![foo][bar]


```

![foo](https://github.githubassets.com/images/modules/logos_page/Octocat.png)

이렇게 사용하면 같은 이미지를 사용할 때 여러 번 같은 경로를 채워 넣는 수고를 줄일 수 있다.

Reference-style에서 label 대소문자 구분은 무시되기 때문에, 아래와 같이 기입해도 정상적으로 작동한다.

```
![foo][bar]


```

![foo](https://github.githubassets.com/images/modules/logos_page/Octocat.png)

### Collapsed

레퍼런스 스타일에서 `title`도 추가할 수 있다. 뒤의 `[`와 `]` 사이에 label을 지정하지 않으면 `alt`에 해당하는 부분을 label처럼 사용할 수 있다.

```
![foo][]


```

![foo](https://github.githubassets.com/images/modules/logos_page/Octocat.png)

`alt` 태그 역시 대소문자를 구별하지 않는다. (case-insensitive하다)

```
![foo][]


```

![foo](https://github.githubassets.com/images/modules/logos_page/Octocat.png)

레퍼런스 링크를 사용할 때, `[]`와 `[]` 사이의 공백은 허용되지 않는다.

```
![foo]
[]


```

![foo](https://github.githubassets.com/images/modules/logos_page/Octocat.png)

[foo](https://github.githubassets.com/images/modules/logos_page/Octocat.png): https://github.githubassets.com/images/modules/logos_page/Octocat.png" 레퍼런스 스타일로 삽입한 깃허브의 로고"*예상과 다른 결과*

link lable은 `[`나 `]`를 포함해선 안 된다.

```
![[foo]]

[[foo]]: https://github.githubassets.com/images/modules/logos_page/Octocat.png "title"
```

!\[[foo](https://github.githubassets.com/images/modules/logos_page/Octocat.png)\]

\[[foo](https://github.githubassets.com/images/modules/logos_page/Octocat.png)\]: https://github.githubassets.com/images/modules/logos_page/Octocat.png "title"

`![foo]`의 형태로 보여주고 싶다면, 아래와 같이 이스케이프 문자 `\`를 사용한다.

```
!\[foo]
```

!\[foo]

---

References
----------

[GFM 공식문서](https://github.github.com/gfm/#images)
