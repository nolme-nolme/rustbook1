# Macros

러스트 매크로는 메타 프로그래밍 기능으로 컴파일 과정에서 AST에 기초하여 생성한다. 러스트 매크로는 패턴 매칭을 사용하여 코드 생성을 한다.&#x20;

러스트 매크로는 선언적 매크로 (declarative macro 또는 macro by example)와 절차적 매크로 (procedural macro)가 있다.&#x20;

rust-lang의 매크로 설명이 간략하여 레퍼런스에 있는 내용을 기초로 하여 정리하고 부족하거나 어려운 부분은 The little book of rust macros를 참고한다.&#x20;

## 선언적 매크로&#x20;



**Syntax**\
_MacroRulesDefinition_ :\
&#x20;  `macro_rules` `!` [IDENTIFIER](https://doc.rust-lang.org/reference/identifiers.html) _MacroRulesDef_

_MacroRulesDef_ :\
&#x20;     `(` _MacroRules_ `)` `;`\
&#x20;  \| `[` _MacroRules_ `]` `;`\
&#x20;  \| `{` _MacroRules_ `}`

_MacroRules_ :\
&#x20;  _MacroRule_ ( `;` _MacroRule_ )\* `;`?

_MacroRule_ :\
&#x20;  _MacroMatcher_ `=>` _MacroTranscriber_

_MacroMatcher_ :\
&#x20;     `(` _MacroMatch_\* `)`\
&#x20;  \| `[` _MacroMatch_\* `]`\
&#x20;  \| `{` _MacroMatch_\* `}`

_MacroMatch_ :\
&#x20;     [_Token_](https://doc.rust-lang.org/reference/tokens.html)_except `$` and_ [_delimiters_](https://doc.rust-lang.org/reference/tokens.html#delimiters)\
&#x20;  \| _MacroMatcher_\
&#x20;  \| `$` ( [IDENTIFIER\_OR\_KEYWORD](https://doc.rust-lang.org/reference/identifiers.html) _except `crate`_ | [RAW\_IDENTIFIER](https://doc.rust-lang.org/reference/identifiers.html) | `_` ) `:` _MacroFragSpec_\
&#x20;  \| `$` `(` _MacroMatch_+ `)` _MacroRepSep_? _MacroRepOp_

_MacroFragSpec_ :\
&#x20;     `block` | `expr` | `ident` | `item` | `lifetime` | `literal`\
&#x20;  \| `meta` | `pat` | `pat_param` | `path` | `stmt` | `tt` | `ty` | `vis`

_MacroRepSep_ :\
&#x20;  [_Token_](https://doc.rust-lang.org/reference/tokens.html)_except_ [_delimiters_](https://doc.rust-lang.org/reference/tokens.html#delimiters) _and MacroRepOp_

_MacroRepOp_ :\
&#x20;  `*` | `+` | `?`

_MacroTranscriber_ :\
&#x20;  [_DelimTokenTree_](https://doc.rust-lang.org/reference/macros.html)
