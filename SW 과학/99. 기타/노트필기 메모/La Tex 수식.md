>[!cite]- 기본적인 문법 
> <iframe src="https://velog.io/@d2h10s/LaTex-Markdown-%EC%88%98%EC%8B%9D-%EC%9E%91%EC%84%B1%EB%B2%95" frameborder="0" style="width: 100%;height: 800px;"></iframe>


# 이외의 표현들

```latex
\documentclass{standalone}
\usepackage{upquote}% getting the right grave ` (and not ‘)!
\begin{document}
\begin{tabular}{lcc}
Input                   &       Text       &                 Math                  \\ \hline
\verb|\string^|         &     \string^     &              $\string^$               \\
\verb|\char`\^|         &     \char`\^     &              $\char`\^$               \\
\verb|\verb!^!|         &     \verb!^!     &              $\verb!^!$               \\ \hline
\verb|\textasciicircum| & \textasciicircum &                  ---                  \\
\verb|\^{}|             & \^{} (e.g. \^a)  &                  ---                  \\ \hline
\verb|\hat{}|           &       ---        &       $\hat{}$ (e.g. $\hat a$)        \\
\verb|\wedge|           &       ---        &      $\wedge$ (e.g. $a\wedge b$)      \\
\verb|\widehat{}|       &       ---        & $\widehat{\ }$ (e.g. $\widehat{abc}$) \\
\end{tabular}
\end{document}
```
- 물리학  : [벡터 에이위에 모자를 씌워보았다.](http://www.astronomer.rocks/news/articleView.html?idxno=82915)