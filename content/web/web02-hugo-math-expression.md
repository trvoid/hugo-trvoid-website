---
title: "Hugo에서 수학식 쓰기"
---

## MathJax 설정

1. 사용중인 테마의 `layout/partials` 폴더 아래에 `mathjax_support.html` 파일을 만들고 다음 내용을 저장합니다.

	```
	<script type="text/javascript" async
	  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.2/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
	  MathJax.Hub.Config({
	  tex2jax: {
	    inlineMath: [['$','$'], ['\\(','\\)']],
	    displayMath: [['$$','$$']],
	    processEscapes: true,
	    processEnvironments: true,
	    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
	    TeX: { equationNumbers: { autoNumber: "AMS" },
	         extensions: ["AMSmath.js", "AMSsymbols.js"] }
	  }
	  });
	  MathJax.Hub.Queue(function() {
	    // Fix <code> tags after MathJax finishes running. This is a
	    // hack to overcome a shortcoming of Markdown. Discussion at
	    // https://github.com/mojombo/jekyll/issues/199
	    var all = MathJax.Hub.getAllJax(), i;
	    for(i = 0; i < all.length; i += 1) {
	        all[i].SourceElement().parentNode.className += ' has-jax';
	    }
	  });

	  MathJax.Hub.Config({
	  // Autonumbering by mathjax
	  TeX: { equationNumbers: { autoNumber: "AMS" } }
	  });
	</script>
	```

2. 사용중인 테마의 `layout/partials` 폴더 아래에 있는 `custom-footer.html` 파일을 열고 다음 내용을 저장합니다.

	```
	{{ partial "mathjax_support.html" . }}
	```

## 동작 확인

1. `content` 폴더 아래에서 `mathjax-test.md` 파일을 생성하고 다음 내용을 입력합니다.

	```
	<div>
	$$ { h }_{ \theta }(x)={ \theta }_{ 0 }+{ \theta }_{ 1 }{ x }_{ 1 } $$
	</div>
	```

2. 웹사이트 폴더에서 **명령 프롬프트** 창을 열고 Hugo 서버를 실행합니다.

	```
	> hugo server
	```

3. 브라우져로 http://localhost:1313/mathjax-test/ 페이지를 열고 위에서 입력한 방정식이 아래와 같이 표시되는지 확인합니다.

$$ { h }_{ \theta }(x)={ \theta }_{ 0 }+{ \theta }_{ 1 }{ x }_{ 1 } $$

## 참고 자료

1. [Loading and Configuring MathJax](http://docs.mathjax.org/en/latest/configuration.html#loading-and-configuring-mathjax)
2. [Setting MathJax with Hugo](https://divadnojnarg.github.io/blog/mathjax/)
